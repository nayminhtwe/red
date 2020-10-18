<template>
  <div id="cart_popup" class="white-popup-block popup-position">
    <div class="popup-title">
      <h2 class="main_title heading">
        <span>cart</span>
      </h2>
    </div>
    <div class="popup-detail">
      <div class="cart-dropdown ">
        <ul class="cart-list link-dropdown-list">
          <li>
            <a class="close-cart"><i class="fa fa-times-circle" /></a>
            <div class="media">
              <a class="pull-left"> <img alt="Stylexpo" src="/assets/images/1.jpg"></a>
              <div class="media-body">
                <span><a href="#">Black African Print Skirt</a></span>
                <p class="cart-price">
                  $14.99
                </p>
                <div class="product-qty">
                  <label>Qty:</label>
                  <div class="custom-qty">
                    <input type="text" name="qty" maxlength="8" value="1" title="Qty" class="input-text qty">
                  </div>
                </div>
              </div>
            </div>
          </li>
          <li>
            <a class="close-cart"><i class="fa fa-times-circle" /></a>
            <div class="media">
              <a class="pull-left"> <img alt="Stylexpo" src="/assets/images/2.jpg"></a>
              <div class="media-body">
                <span><a href="#">Black African Print Skirt</a></span>
                <p class="cart-price">
                  $14.99
                </p>
                <div class="product-qty">
                  <label>Qty:</label>
                  <div class="custom-qty">
                    <input type="text" name="qty" maxlength="8" value="1" title="Qty" class="input-text qty">
                  </div>
                </div>
              </div>
            </div>
          </li>
        </ul>
        <p class="cart-sub-totle">
          <span class="pull-left">Cart Subtotal</span> <span class="pull-right"><strong class="price-box">$29.98</strong></span>
        </p>
        <div class="clearfix" />
        <div class="mt-20">
          <a href="cart.html" class="btn-color btn">Cart</a> <a href="checkout.html" class="btn-color btn right-side">Checkout</a>
        </div>
      </div>
    </div>
    <button title="Close (Esc)" type="button" class="mfp-close" @click="closeMicrocartExtend">
      ×
    </button>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import i18n from '@vue-storefront/i18n'
import { isModuleRegistered } from '@vue-storefront/core/lib/modules'
import { currentStoreView } from '@vue-storefront/core/lib/multistore'

import VueOfflineMixin from 'vue-offline/mixin'
import onEscapePress from '@vue-storefront/core/mixins/onEscapePress'
import InstantCheckout from 'src/modules/instant-checkout/components/InstantCheckout.vue'
import { registerModule } from '@vue-storefront/core/lib/modules'

import BaseInput from 'theme/components/core/blocks/Form/BaseInput'
import ClearCartButton from 'theme/components/core/blocks/Microcart/ClearCartButton'
import ButtonFull from 'theme/components/theme/ButtonFull'
import ButtonOutline from 'theme/components/theme/ButtonOutline'
import Product from 'theme/components/core/blocks/Microcart/Product'
import EditMode from './EditMode'
import { InstantCheckoutModule } from 'src/modules/instant-checkout'

export default {
  name: 'Microcart',
  components: {
    Product,
    ClearCartButton,
    ButtonFull,
    ButtonOutline,
    BaseInput,
    InstantCheckout
  },
  mixins: [
    VueOfflineMixin,
    EditMode,
    onEscapePress
  ],
  data () {
    return {
      addCouponPressed: false,
      couponCode: '',
      componentLoaded: false,
      isInstantCheckoutRegistered: isModuleRegistered('InstantCheckoutModule')
    }
  },
  props: {
    isCheckoutMode: {
      type: Boolean,
      required: false,
      default: () => false
    }
  },
  beforeCreate () {
    registerModule(InstantCheckoutModule)
  },
  mounted () {
    this.$nextTick(() => {
      this.componentLoaded = true
    })
  },
  computed: {
    ...mapGetters({
      productsInCart: 'cart/getCartItems',
      appliedCoupon: 'cart/getCoupon',
      totals: 'cart/getTotals',
      isOpen: 'cart/getIsMicroCartOpen'
    }),
    storeView () {
      return currentStoreView()
    }
  },
  methods: {
    ...mapActions({
      applyCoupon: 'cart/applyCoupon'
    }),
    addDiscountCoupon () {
      this.addCouponPressed = true
    },
    clearCoupon () {
      this.$store.dispatch('cart/removeCoupon')
      this.addCouponPressed = false
    },
    toggleMicrocart () {
      this.$store.dispatch('ui/toggleMicrocart')
    },
    async setCoupon () {
      const couponApplied = await this.applyCoupon(this.couponCode)
      this.addCouponPressed = false
      this.couponCode = ''
      if (!couponApplied) {
        this.$store.dispatch('notification/spawnNotification', {
          type: 'warning',
          message: i18n.t("You've entered an incorrect coupon code. Please try again."),
          action1: { label: i18n.t('OK') }
        })
      }
    },
    closeMicrocartExtend () {
      this.toggleMicrocart()
      this.$store.commit('ui/setSidebar', false)
      this.addCouponPressed = false
    },
    onEscapePress () {
      this.$store.dispatch('ui/closeMicrocart')
    },
    clearCart () {
      this.$store.dispatch('notification/spawnNotification', {
        type: 'warning',
        message: i18n.t('Are you sure you would like to remove all the items from the shopping cart?'),
        action1: { label: i18n.t('Cancel'), action: 'close' },
        action2: { label: i18n.t('OK'),
          action: async () => {
            // We just need to clear cart on frontend and backend.
            // but cart token can be reused
            await this.$store.dispatch('cart/clear', { disconnect: false })
          }
        },
        hasNoTimeout: true
      })
    }
  }
}
</script>
