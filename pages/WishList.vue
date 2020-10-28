<template>
  <section class="ptb-70">
    <div class="container">
      <div class="row">
        <div class="col-12 ">
          <div class="cart-item-table commun-table">
            <div class="table-responsive">
              <table class="table">
                <thead>
                  <tr>
                    <th>Product</th>
                    <th>Descriotion</th>
                    <th>Price</th>
                    <!-- <th>Quantity</th> -->
                    <th>Stock Status</th>
                    <th>Action</th>
                  </tr>
                </thead>
                <tbody v-if="productsInWishlist.length">
                  <product v-for="wishlistProduct in productsInWishlist" :key="wishlistProduct.id" :product="wishlistProduct" />
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
              <!-- <a href="shop.html" class="btn btn-color">
                <span><i class="fa fa-angle-left" /></span>Continue Shopping
              </a> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Wishlist from '@vue-storefront/core/compatibility/components/blocks/Wishlist/Wishlist'
import Product from 'theme/components/core/blocks/Wishlist/Product'
import ClearWishlistButton from 'theme/components/core/blocks/Wishlist/ClearWishlistButton'

export default {
  props: {
    product: {
      type: Object,
      required: false,
      default: () => { }
    }
  },
  components: {
    Product,
    ClearWishlistButton
  },
  methods: {
    clearWishlist () {
      this.$store.dispatch('notification/spawnNotification', {
        type: 'warning',
        message: this.$t('Are you sure you would like to remove all the items from the wishlist?'),
        action1: { label: this.$t('OK'),
          action: () => {
            this.$store.dispatch('wishlist/clear')
          }
        },
        action2: { label: this.$t('Cancel'), action: 'close' },
        hasNoTimeout: true
      })
    }
  },
  mixins: [Wishlist]
}
</script>
