<template>
  <no-ssr>
    <carousel :items="1" :loop="true" :autoplay="true" :dots="true" :center="true" :nav="false">
      <div class="banner-3">
        <img src="/assets/images/banner3.jpg" alt="Stylexpo">
        <div class="banner-detail">
          <div class="container">
            <div class="row">
              <div class="col-lg-5 col-md-5 col-4" />
              <div class="col-lg-7 col-md-7 col-8">
                <div class="banner-detail-inner">
                  <span class="slogan">UP TO 30% OFF</span>
                  <h1 class="banner-title">
                    Collection for women
                  </h1>
                  <span class="offer">Beauty from a great selection</span>
                </div>
                <a class="btn btn-color" href="shop.html">Shop Now!</a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="banner-1">
        <img src="/assets/images/banner1.jpg" alt="Stylexpo">
        <div class="banner-detail">
          <div class="container">
            <div class="row">
              <div class="col-lg-5 col-4" />
              <div class="col-lg-7 col-8">
                <div class="banner-detail-inner">
                  <span class="slogan">UP TO 25% OFF</span>
                  <h1 class="banner-title">
                    More Fashion Styles
                  </h1>
                  <span class="offer">The latest fashion trends online.</span>
                </div>
                <a class="btn btn-color" href="shop.html">Shop Now!</a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="banner-2">
        <img src="/assets/images/banner2.jpg" alt="Stylexpo">
        <div class="banner-detail">
          <div class="container">
            <div class="row">
              <div class="col-lg-1" />
              <div class="col-lg-8 col-8">
                <div class="banner-detail-inner">
                  <span class="slogan">new look</span>
                  <h1 class="banner-title">
                    fashion Week 2019
                  </h1>
                  <span class="offer">Popular Brand Products 20% off</span>
                </div>
                <a class="btn btn-color" href="shop.html">Shop Now!</a>
              </div>
              <div class="col-lg-3 col-4" />
            </div>
          </div>
        </div>
      </div>

      <div class="banner-3">
        <img src="/assets/images/banner3.jpg" alt="Stylexpo">
        <div class="banner-detail">
          <div class="container">
            <div class="row">
              <div class="col-lg-5 col-md-5 col-4" />
              <div class="col-lg-7 col-md-7 col-8">
                <div class="banner-detail-inner">
                  <span class="slogan">UP TO 30% OFF</span>
                  <h1 class="banner-title">
                    Collection for women
                  </h1>
                  <span class="offer">Beauty from a great selection</span>
                </div>
                <a class="btn btn-color" href="shop.html">Shop Now!</a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="banner-1">
        <img src="/assets/images/banner1.jpg" alt="Stylexpo">
        <div class="banner-detail">
          <div class="container">
            <div class="row">
              <div class="col-lg-5 col-4" />
              <div class="col-lg-7 col-8">
                <div class="banner-detail-inner">
                  <span class="slogan">UP TO 25% OFF</span>
                  <h1 class="banner-title">
                    More Fashion Styles
                  </h1>
                  <span class="offer">The latest fashion trends online.</span>
                </div>
                <a class="btn btn-color" href="shop.html">Shop Now!</a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="banner-2">
        <img src="/assets/images/banner2.jpg" alt="Stylexpo">
        <div class="banner-detail">
          <div class="container">
            <div class="row">
              <div class="col-lg-1" />
              <div class="col-lg-8 col-8">
                <div class="banner-detail-inner">
                  <span class="slogan">new look</span>
                  <h1 class="banner-title">
                    fashion Week 2019
                  </h1>
                  <span class="offer">Popular Brand Products 20% off</span>
                </div>
                <a class="btn btn-color" href="shop.html">Shop Now!</a>
              </div>
              <div class="col-lg-3 col-4" />
            </div>
          </div>
        </div>
      </div>
    </carousel>
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
