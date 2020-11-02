<template>
  <section class="ptb-70" v-if="products.length > 0">
    <div class="container">
      <div class="product-listing">
        <div class="row">
          <div class="col-12">
            <div class="heading-part mb-30">
              <h2 class="main_title heading">
                <span>{{ name }}</span>
              </h2>
            </div>
          </div>
        </div>
        <div class="pro_cat">
          <div class="row">
            <div class="col-12">
              <div class="best-seller-pro" id="brand-logo">
                <carousel :items="5" :loop="true" :responsive-class="true"
                          :autoplay="false" :dots="false"
                          :nav="true" :responsive="{0:{items:2},501:{items:2},768:{items:3},992:{items:4},1500:{items:5}}"
                >
                  <div class="item" v-for="product in products" :key="product.id">
                    <product-tile :product="product" />
                  </div>
                  <div class="item" v-for="product in products" :key="product.id">
                    <product-tile :product="product" />
                  </div>
                </carousel>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// import ButtonOutline from 'theme/components/theme/ButtonOutline'
import ProductTile from 'theme/components/core/ProductTile'
import NoSSR from 'vue-no-ssr'

export default {
  components: {
    // ButtonOutline
    'carousel': typeof document !== 'undefined' ? () => import('vue-owl-carousel') : '',
    ProductTile
  },
  props: {
    products: {
      type: null,
      required: true
    },
    name: {
      type: null,
      required: true
    }
  }
}
</script>
