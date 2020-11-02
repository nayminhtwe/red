<template>
  <div class="product-item" v-observe-visibility="visibilityChanged">
    <div class="row ">
      <div class="col-md-6 col-12 deals-img ">
        <div class="product-image">
          <router-link
            :to="productLink"
            data-testid="productLink"
          >
            <product-image
              class="product-cover__thumb"
              :image="thumbnailObj"
              :alt="product.name | htmlDecode"
              :calc-ratio="false"
              data-testid="productImage"
            />
            <img src="/assets/images/2.jpg" alt="Stylexpo">
            <!-- <img :src="thumbnailObj.src" alt="Stylexpo"> -->
          </router-link>
        </div>
      </div>
      <div class="col-md-6 col-12 mt-xs-30">
        <div class="product-item-details">
          <div class="product-item-name">
            <router-link
              :to="productLink"
              data-testid="productLink"
            >
              {{ product.name | htmlDecode }}
            </router-link>
          </div>
          <div class="price-box" v-if="product.special_price && parseFloat(product.original_price_incl_tax) > 0 && !onlyImage">
            <span class="price">{{ product.price_incl_tax | price(storeView) }}</span><del class="price old-price">{{ product.original_price_incl_tax | price(storeView) }}</del>
          </div>
          <div class="price-box" v-if="!product.special_price && parseFloat(product.price_incl_tax) > 0 && !onlyImage">
            <span class="price">{{ product.price_incl_tax | price(storeView) }}</span>
          </div>
          <p v-html="product.short_description" />
        </div>
        <div class="product-detail-inner">
          <div class="detail-inner-left">
            <ul>
              <li class="pro-cart-icon">
                <add-to-cart
                  :product="product"
                  :disabled="isAddToCartDisabled"
                />
              </li>
              <li class="pro-wishlist-icon active">
                <AddToWishlist :product="product" />
              </li>
              <li class="pro-compare-icon">
                <a href="compare.html" title="Compare" />
              </li>
            </ul>
          </div>
        </div>
        <div class="item-offer-clock">
          <ul class="countdown-clock">
            <li>
              <span class="days">{{ days }}</span>
              <p class="days_ref">
                days
              </p>
            </li>
            <li class="seperator">
              :
            </li>
            <li>
              <span class="hours">{{ hours }}</span>
              <p class="hours_ref">
                hours
              </p>
            </li>
            <li class="seperator">
              :
            </li>
            <li>
              <span class="minutes">{{ minutes }}</span>
              <p class="minutes_ref">
                minutes
              </p>
            </li>
            <li class="seperator">
              :
            </li>
            <li>
              <span class="seconds">{{ seconds }}</span>
              <p class="seconds_ref">
                seconds
              </p>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import rootStore from '@vue-storefront/core/store'
import { ProductTile } from '@vue-storefront/core/modules/catalog/components/ProductTile.ts'
import config from 'config'
import ProductImage from './ProductImage'
import AddToWishlist from 'theme/components/core/blocks/Wishlist/AddToWishlist'
import AddToCompare from 'theme/components/core/blocks/Compare/AddToCompare'
import { IsOnWishlist } from '@vue-storefront/core/modules/wishlist/components/IsOnWishlist'
import { IsOnCompare } from '@vue-storefront/core/modules/compare/components/IsOnCompare'
import { currentStoreView } from '@vue-storefront/core/lib/multistore'
import AddToCart from 'theme/components/core/AddToCart'

export default {
  name: 'CountdownProductTile',
  data () {
    return {
      days: 0,
      hours: 0,
      minutes: 0,
      seconds: 0

    };
  },
  mixins: [ProductTile, IsOnWishlist, IsOnCompare],
  components: {
    ProductImage,
    AddToWishlist,
    AddToCompare,
    AddToCart
    // VueCountdownTimer
    // 'vue-countdown-timer': typeof window !== 'undefined' ? () => import('vuejs-countdown-timer') : ''
  },
  props: {
    labelsActive: {
      type: Boolean,
      default: true
    },
    onlyImage: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    thumbnailObj () {
      return {
        src: this.thumbnail,
        loading: this.thumbnail
      }
    },
    favoriteIcon () {
      return this.isOnWishlist ? 'favorite' : 'favorite_border'
    },
    storeView () {
      return currentStoreView()
    }
  },
  methods: {
    onProductPriceUpdate (product) {
      if (product.sku === this.product.sku) {
        Object.assign(this.product, product)
      }
    },
    visibilityChanged (isVisible, entry) {
      if (
        isVisible &&
        config.products.configurableChildrenStockPrefetchDynamic &&
        config.products.filterUnavailableVariants &&
        this.product.type_id === 'configurable' &&
        this.product.configurable_children &&
        this.product.configurable_children.length > 0
      ) {
        const skus = [this.product.sku]
        for (const confChild of this.product.configurable_children) {
          const cachedItem = rootStore.state.stock.cache[confChild.id]
          if (typeof cachedItem === 'undefined' || cachedItem === null) {
            skus.push(confChild.sku)
          }
        }
        if (skus.length > 0) {
          rootStore.dispatch('stock/list', { skus: skus }) // store it in the cache
        }
      }
    },
    countDown () {
      if (this.seconds > 0) {
        this.seconds--
      } else if (this.seconds === 0) {
        if (this.minutes > 0) {
          this.minutes--;
          this.seconds = 59;
        } else if (this.minutes === 0) {
          if (this.hours > 24) {
            this.hours--;
            this.minutes = 59;
            this.seconds = 59;
          } else if (this.hours === 0) {
            this.days--;
            this.hours = 23;
            this.minutes = 59;
            this.seconds = 59;
          }
        }
      }
    }
  },
  beforeMount () {
    this.$bus.$on('product-after-priceupdate', this.onProductPriceUpdate)
  },
  created () {
    let date_future = new Date(new Date().getFullYear() + 1, 0, 1);
    let date_now = new Date();

    let seconds = Math.floor((date_future - (date_now)) / 1000);
    let minutes = Math.floor(seconds / 60);
    let hours = Math.floor(minutes / 60);
    let days = Math.floor(hours / 24);

    this.days = days;
    this.seconds = Math.floor((((date_future - (date_now)) % 1000) * 60) / 1000);
    this.minutes = Math.floor(seconds % 60);
    this.hours = Math.floor(minutes % 60);
  },
  mounted () {
    this.$nextTick(function () {
      window.setInterval(() => {
        this.countDown();
      }, 1000);
    })
  },
  beforeDestroy () {
    this.$bus.$off('product-after-priceupdate', this.onProductPriceUpdate)
  }
}
</script>
