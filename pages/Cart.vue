<template>
  <section class="ptb-70">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <div class="cart-item-table commun-table">
            <div class="table-responsive">
              <table class="table">
                <thead>
                  <tr>
                    <th>Product</th>
                    <th>Product Name</th>
                    <th>Price</th>
                    <th>Quantity</th>
                    <th>Sub Total</th>
                    <th>Action</th>
                  </tr>
                </thead>
                <tbody>
                  <table-product v-for="product in productsInCart" :key="product.server_item_id || product.id" :product="product" component="cart" />
                  <!-- <product v-for="product in productsInCart" :key="product.server_item_id || product.id" :product="product" component="cart" /> -->

                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
      <div class="mb-30">
        <div class="row">
          <div class="col-md-6">
            <div class="mt-30">
              <router-link :to="localizedRoute('/')" class="btn btn-color">
                <span><i class="fa fa-angle-left" /></span>Continue Shopping
              </router-link>
            </div>
          </div>
          <div class="col-md-6">
            <div class="mt-30 right-side float-none-xs">
              <router-link :to="{ name: 'checkout' }" class="btn btn-color">
                Checkout
              </router-link>
            </div>
          </div>
        </div>
      </div>
      <hr>
      <div class="mtb-30">
        <div class="row">
          <div class="col-md-6 mb-xs-40">
            <div class="estimate">
              <div class="heading-part mb-20">
                <h3 class="sub-heading">
                  {{ $t('Discount code') }}
                </h3>
              </div>
              <form class="full">
                <div class="row">
                  <div class="col-md-6">
                    <div class="input-box select-dropdown mb-20">
                      <div v-if="OnlineOnly" class="col-xs-12 pt30 coupon-wrapper">
                        <div class="coupon-input">
                          <!-- <label class="h6 cl-secondary">{{ $t('Discount code') }}</label> -->
                          <base-input type="text" id="couponinput" :autofocus="true" v-model.trim="couponCode" @keyup.enter="setCoupon" />
                        </div>
                        <button class="btn btn-color" :disabled="!couponCode" @click.prevent="setCoupon">
                          {{ $t('Add discount code') }}
                        </button>
                      </div>
                    </div>
                  </div>
                </div>
              </form>
            </div>
          </div>
          <div class="col-md-6">
            <div class="cart-total-table commun-table">
              <div class="table-responsive">
                <table class="table">
                  <thead>
                    <tr>
                      <th colspan="2">
                        Cart Total
                      </th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(segment, index) in totals">
                      <td>{{ segment.title }}</td>
                      <td>
                        <div class="price-box">
                          <span class="price">{{ segment.value | price(storeView) }}</span>
                        </div>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
      <hr>
      <div class="mt-30">
        <div class="row">
          <div class="col-12">
            <div class="right-side float-none-xs">
              <router-link :to="{ name: 'checkout' }" class="btn btn-color">
                Checkout <span><i class="fa fa-angle-right" /></span>
              </router-link>
              <!-- <a href="checkout.html" class="btn btn-color">Proceed to checkout
                <span><i class="fa fa-angle-right" /></span>
              </a> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
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
import TableProduct from 'theme/components/core/blocks/Microcart/TableProduct'
import { InstantCheckoutModule } from 'src/modules/instant-checkout'

export default {
  name: 'Cart',
  components: {
    // Product,
    TableProduct,
    ClearCartButton,
    ButtonFull,
    ButtonOutline,
    BaseInput,
    InstantCheckout
  },
  mixins: [
    VueOfflineMixin,
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
