<template>
  <tr>
    <td>
      <router-link :to="productLink">
        <product-image :image="image" />
      </router-link>
    </td>
    <td>
      <div class="product-title">
        <router-link :to="productLink">
          {{ product.name | htmlDecode }}
        </router-link>
        <div class="size-text">
          <span>{{ product.sku }}</span>
        </div>
      </div>
    </td>
    <td>
      <ul>
        <li>
          <div class="base-price price-box">
            <span class="price">{{ product.price_incl_tax | price(storeView) }}</span>
          </div>
        </li>
      </ul>
    </td>
    <!-- <td>
      <div class="input-box select-dropdown">
        <fieldset>
          <select data-id="100" class="quantity_cart option-drop" name="quantity_cart" id="ui-id-5" style="display: none;">
            <option selected="" value="1">
              1
            </option>
            <option value="2">
              2
            </option>
            <option value="3">
              3
            </option>
            <option value="4">
              4
            </option>
          </select><span class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all" tabindex="0" id="ui-id-5-button" role="combobox" aria-expanded="false" aria-autocomplete="list" aria-owns="ui-id-5-menu" aria-haspopup="true" aria-activedescendant="ui-id-7" aria-labelledby="ui-id-7" aria-disabled="false" style="width: 100px;"><span class="ui-icon ui-icon-triangle-1-s" /><span class="ui-selectmenu-text">1</span></span>
        </fieldset>
      </div>
    </td> -->
    <td>
      <div class="total-price price-box">
        <span class="price">In Stock</span>
      </div>
    </td>
    <td>
      <add-to-cart
        v-if="product.type_id === 'simple'"
        :product="product"
      />

      <i title="Remove Item From Cart" data-id="100" class="fa fa-trash cart-remove-item" @click="removeProductFromWhishList(product)" />
    </td>
  </tr>
</template>

<script>
import config from 'config'
import Product from '@vue-storefront/core/compatibility/components/blocks/Wishlist/Product'
import { currentStoreView } from '@vue-storefront/core/lib/multistore'
import { formatProductLink } from '@vue-storefront/core/modules/url/helpers'
import ProductImage from 'theme/components/core/ProductImage'
import RemoveButton from './RemoveButton'
import i18n from '@vue-storefront/i18n'
import { htmlDecode } from '@vue-storefront/core/lib/store/filters'
import AddToCart from './AddToCart'

export default {
  components: {
    RemoveButton,
    ProductImage,
    AddToCart
  },
  mixins: [Product],
  props: {
    showAddToCart: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    productLink () {
      return formatProductLink(this.product, currentStoreView().storeCode)
    },
    image () {
      return {
        loading: this.thumbnail,
        src: this.thumbnail
      }
    },
    storeView () {
      return currentStoreView()
    }
  },
  methods: {
    removeProductFromWhishList (product) {
      this.$store.dispatch('notification/spawnNotification', {
        type: 'success',
        message: i18n.t('Product {productName} has been removed from wishlist!', { productName: htmlDecode(product.name) }),
        action1: { label: i18n.t('OK') }
      }, { root: true })
      this.removeFromWishlist(product)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~theme/css/animations/transitions';
.blend {
  flex: 0 0 121px;
  opacity: .8;
  will-change: opacity;
  transition: .3s opacity $motion-main;
  &:hover{
     opacity: 1;
   }
}
.col-xs {
  flex-direction: column;
}
input {
  width: 30px;
}
.price-original {
  text-decoration: line-through;
  color: #828282;
  font-size: .95rem;
}
.wishlist-add-to-cart {
  padding: 10px;
  margin: 15px 0;
  min-width: 100px;
  font-size: 14px;
  text-align: center;
}
.price-original {
  text-decoration: line-through;
  color: #828282;
  font-size: .95rem;
}
.price-original {
  text-decoration: line-through;
  color: #828282;
  font-size: .95rem;
}
</style>
