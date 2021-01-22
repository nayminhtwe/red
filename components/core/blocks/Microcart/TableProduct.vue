<template>
  <tr>
    <td>
      <router-link :to="productLink">
        <product-image :image="image" />
      </router-link>
    </td>
    <td>
      <router-link :to="productLink">{{ product.name | htmlDecode }}</router-link>
    </td>
    <td>
      <ul>
        <li>
          <div
            class="base-price price-box"
            v-if="product.special_price && parseFloat(product.original_price_incl_tax) > 0 && !onlyImage"
          >
            <span class="price">{{ product.price_incl_tax | price(storeView) }}</span>
            <del class="price old-price">{{ product.original_price_incl_tax | price(storeView) }}</del>
          </div>
          <div
            class="base-price price-box"
            v-if="!product.special_price && parseFloat(product.price_incl_tax) > 0 && !onlyImage"
          >
            <span class="price">{{ product.price_incl_tax | price(storeView) }}</span>
          </div>
        </li>
      </ul>
    </td>
    <td>
      <div class="input-box select-dropdown">
        <product-quantity
          :value="productQty"
          :max-quantity="maxQuantity"
          :loading="isStockInfoLoading"
          :is-simple-or-configurable="isSimpleOrConfigurable"
          @input="updateProductQty"
          @error="handleQuantityError"
        />
      </div>
    </td>
    <td>
      <div class="total-price price-box">
        <span class="price">{{ product.price_incl_tax * product.qty | price(storeView) }}</span>
      </div>
    </td>
    <td>
      <remove-button :component="component" @click="removeItem" />
    </td>
  </tr>
</template>

<script>
import { mapActions, mapState } from "vuex";
import config from "config";
import { currentStoreView } from "@vue-storefront/core/lib/multistore";
import { formatProductLink } from "@vue-storefront/core/modules/url/helpers";
import Product from "@vue-storefront/core/compatibility/components/blocks/Microcart/Product";

import ProductQuantity from "theme/components/core/ProductQuantity.vue";
import ProductImage from "theme/components/core/ProductImage";
import ColorSelector from "theme/components/core/ColorSelector.vue";
import SizeSelector from "theme/components/core/SizeSelector.vue";
import RemoveButton from "./RemoveButton";
import EditButton from "./EditButton";
import { onlineHelper } from "@vue-storefront/core/helpers";
import { ProductOption } from "@vue-storefront/core/modules/catalog/components/ProductOption";
import {
  getThumbnailForProduct,
  getProductConfiguration
} from "@vue-storefront/core/modules/cart/helpers";
import ButtonFull from "theme/components/theme/ButtonFull";
import EditMode from "./EditMode";

export default {
  name: "TableProduct",
  data() {
    return {
      maxQuantity: 0,
      quantityError: false,
      isStockInfoLoading: false
    };
  },
  props: {
    product: {
      type: Object,
      required: true
    },
    component: {
      type: String,
      required: true
    }
  },
  components: {
    RemoveButton,
    ProductImage,
    ColorSelector,
    SizeSelector,
    EditButton,
    ButtonFull,
    ProductQuantity
  },
  mixins: [Product, ProductOption, EditMode],
  computed: {
    ...mapState({
      isMicrocartOpen: state => state.ui.microcart
    }),
    hasProductInfo() {
      return this.product.info && Object.keys(this.product.info).length > 0;
    },
    hasProductErrors() {
      const errors = this.product.errors || {};
      const errorsValuesExists =
        Object.keys(errors).filter(errorKey => errors[errorKey]).length > 0;
      return errorsValuesExists;
    },
    isTotalsActive() {
      return (
        this.isOnline &&
        !this.editMode &&
        this.product.totals &&
        this.product.totals.options
      );
    },
    isOnline() {
      return onlineHelper.isOnline;
    },
    productsAreReconfigurable() {
      return (
        config.cart.productsAreReconfigurable &&
        this.product.type_id === "configurable" &&
        this.isOnline
      );
    },
    displayItemDiscounts() {
      return config.cart.displayItemDiscounts;
    },
    image() {
      return {
        loading: this.thumbnail,
        src: this.thumbnail
      };
    },
    thumbnail() {
      return getThumbnailForProduct(this.product);
    },
    configuration() {
      return getProductConfiguration(this.product);
    },
    productLink() {
      return formatProductLink(this.product, currentStoreView().storeCode);
    },
    editMode() {
      return this.getEditingProductId === this.product.id;
    },
    productQty() {
      return this.editMode ? this.getEditingQty : this.product.qty;
    },
    isSimpleOrConfigurable() {
      return ["simple", "configurable"].includes(this.product.type_id);
    },
    isUpdateCartDisabled() {
      return (
        this.quantityError ||
        this.isStockInfoLoading ||
        (this.isOnline && !this.maxQuantity && this.isSimpleOrConfigurable)
      );
    },
    storeView() {
      return currentStoreView();
    }
  },
  async beforeMount() {
    if (this.isOnline) {
      const maxQuantity = await this.getQuantity();
      this.maxQuantity = maxQuantity;
    }
  },
  methods: {
    updateProductVariant() {
      this.updateVariant();
      this.closeEditMode();
    },
    updateProductQty(qty) {
      if (this.editMode) {
        this.editModeSetQty(qty);
        return;
      }

      this.updateQuantity(qty);
    },
    removeFromCart() {
      this.$store.dispatch("cart/removeItem", { product: this.product });
    },
    updateQuantity(quantity) {
      this.$store.dispatch("cart/updateQuantity", {
        product: this.product,
        qty: quantity
      });
    },
    async getQuantity(product) {
      if (this.isStockInfoLoading) return; // stock info is already loading
      this.isStockInfoLoading = true;
      try {
        const validProduct = product || this.product;
        const res = await this.$store.dispatch("stock/check", {
          product: validProduct,
          qty: this.productQty
        });
        return res.qty;
      } finally {
        this.isStockInfoLoading = false;
      }
    },
    handleQuantityError(error) {
      this.quantityError = error;
    },
    async changeEditModeFilter(filter) {
      const editedProduct = this.getEditedProduct(filter);
      const maxQuantity = await this.getQuantity(editedProduct);
      if (!maxQuantity) {
        this.$store.dispatch("notification/spawnNotification", {
          type: "error",
          message: this.$t(
            "The product is out of stock and cannot be added to the cart!"
          ),
          action1: { label: this.$t("OK") }
        });
      } else if (maxQuantity < this.productQty) {
        this.$store.dispatch("notification/spawnNotification", {
          type: "error",
          message: this.$t(
            "Only {maxQuantity} products of this type are available!",
            { maxQuantity }
          ),
          action1: { label: this.$t("OK") }
        });
      } else {
        this.maxQuantity = maxQuantity;
        this.editModeSetFilters(filter);
      }
    }
  },
  watch: {
    isOnline: {
      async handler(isOnline) {
        if (isOnline) {
          const maxQuantity = await this.getQuantity();
          this.maxQuantity = maxQuantity;
        }
      }
    },
    isMicrocartOpen: {
      async handler(isOpen) {
        if (isOpen) {
          const maxQuantity = await this.getQuantity();
          this.maxQuantity = maxQuantity;
        }
      },
      immediate: true
    }
  }
};
</script>
