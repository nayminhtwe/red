<template>
  <section class=" ptb-70" v-if="products.length > 0">
    <div class="container">
      <div class="daily-deals">
        <div class="row m-0">
          <div class="col-12 p-0">
            <div class="heading-part mb-30">
              <h2 class="main_title heading">
                <span>Daily Deals</span>
              </h2>
            </div>
          </div>
        </div>
        <div class="pro_cat">
          <div class="row">
            <div class="col-12">
              <div id="brand-logo">
                <carousel :items="2" :loop="true" :responsive-class="true"
                          :autoplay="false" :dots="false"
                          :nav="true" :responsive="{0:{items:1},501:{items:1},768:{items:1},992:{items:2},1500:{items:2}}"
                >
                  <div class="item" v-for="product in products" :key="product.id">
                    <countdown-product-tile :product="product" />
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
import CountdownProductTile from 'theme/components/core/CountdownProductTile'
import ProductTile from 'theme/components/core/ProductTile'
import NoSSR from 'vue-no-ssr'

export default {
  components: {
    // ButtonOutline
    'carousel': typeof document !== 'undefined' ? () => import('vue-owl-carousel') : '',
    CountdownProductTile
  },
  props: {
    products: {
      type: null,
      required: true
    }
  }
}
</script>
