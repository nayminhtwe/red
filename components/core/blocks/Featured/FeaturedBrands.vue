<template>
  <no-ssr>
    <div class="brand-logo">
      <div class="container">
        <div class="row">
          <div class="col-12 ">
            <div class="heading-part mb-30">
              <h2 class="main_title heading">
                <span>Our Brands</span>
              </h2>
            </div>
          </div>
        </div>
        <div class="row brand">
          <div class="col-md-12">
            <div id="brand-logo" class="align_center">
              <carousel :items="6" :loop="true" :responsiveClass="true"
                        :autoplay="false" :dots="false"
                        :nav="true" :responsive="{0:{items:1},480:{items:2},768:{items:3},1200:{items:4},1500:{items:6}}"
              >
                <div class="item">
                  <a href="#"><img src="/assets/images/brand1.png" alt="Stylexpo"></a>
                </div>
                <div class="item">
                  <a href="#"><img src="/assets/images/brand2.png" alt="Stylexpo"></a>
                </div>
                <div class="item">
                  <a href="#"><img src="/assets/images/brand3.png" alt="Stylexpo"></a>
                </div>
                <div class="item">
                  <a href="#"><img src="/assets/images/brand4.png" alt="Stylexpo"></a>
                </div>
                <div class="item">
                  <a href="#"><img src="/assets/images/brand5.png" alt="Stylexpo"></a>
                </div>
                <div class="item">
                  <a href="#"><img src="/assets/images/brand6.png" alt="Stylexpo"></a>
                </div>
                <div class="item">
                  <a href="#"><img src="/assets/images/brand7.png" alt="Stylexpo"></a>
                </div>
                <div class="item">
                  <a href="#"><img src="/assets/images/brand8.png" alt="Stylexpo"></a>
                </div>
              </carousel>
            </div>
          </div>
        </div>
      </div>
    </div>
  </no-ssr>
</template>

<script>
// import ButtonOutline from 'theme/components/theme/ButtonOutline'
import { mapGetters } from 'vuex'
import NoSSR from 'vue-no-ssr'

export default {
  components: {
    // ButtonOutline
    'no-ssr': NoSSR,
    'carousel': typeof document !== 'undefined' ? () => import('vue-owl-carousel') : ''
  },
  data () {
    return {
    }
  },
  computed: {
    ...mapGetters({
      currentImage: 'promoted/getHeadImage'
    })
  }
}
</script>

<style lang="scss" scoped>
  .owl-carousel .owl-item img {
    width: auto;
    display: inline-block;
}
</style>
