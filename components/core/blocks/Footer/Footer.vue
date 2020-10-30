<template>
  <div class="footer">
    <div class="container">
      <div class="footer-inner">
        <div class="footer-middle">
          <div class="row">
            <div class="col-xl-3 f-col">
              <div class="footer-static-block">
                <span class="opener plus" @click="toggleFooter('blockOne')" />
                <div class="f-logo">
                  <a href="index.html" class="">
                    <img src="/assets/images/logo.png" alt="Stylexpo">
                  </a>
                </div>
                <div class="footer-block-contant" ref="blockOne">
                  <p>Lorem khaled ipsum is a major key to success. It’s on you how you want to live your life. Always remember in the jungle there’s a lot of they in.</p>
                  <p>It’s on you how you want to live your life. Everyone has a choice.</p>
                </div>
              </div>
            </div>
            <div class="col-xl-3 f-col">
              <div class="footer-static-block">
                <span class="opener plus" @click="toggleFooter('blockTwo')" />
                <h3 class="title">
                  Help <span />
                </h3>
                <ul class="footer-block-contant link" ref="blockTwo">
                  <li><a href="#">Gift Cards</a></li>
                  <li><a href="#">Order Status</a></li>
                  <li><a href="#">Free Shipping</a></li>
                  <li><a href="#">Return & Exchange </a></li>
                  <li><a href="#">International</a></li>
                </ul>
              </div>
            </div>
            <div class="col-xl-3 f-col">
              <div class="footer-static-block">
                <span class="opener plus" @click="toggleFooter('blockThree')" />
                <h3 class="title">
                  Guidance <span />
                </h3>
                <ul class="footer-block-contant link" ref="blockThree">
                  <li><a href="#"> Delivery information</a></li>
                  <li><a href="#"> Privacy Policy</a></li>
                  <li><a href="#"> Terms & Conditions</a></li>
                  <li><a href="#"> Contact</a></li>
                  <li><a href="#"> Sitemap</a></li>
                </ul>
              </div>
            </div>
            <div class="col-xl-3 f-col">
              <div class="footer-static-block" @click="toggleFooter('blockFour')">
                <span class="opener plus" />
                <h3 class="title">
                  address<span />
                </h3>
                <ul class="footer-block-contant address-footer" ref="blockFour">
                  <li class="item">
                    <i class="fa fa-map-marker" />
                    <p>150-A Appolo aprtment, opp. Hopewell Junction, <br>Allen st Road, new york-405001.</p>
                  </li>
                  <li class="item">
                    <i class="fa fa-envelope" />
                    <p> <a href="#">infoservices@stylexpo.com </a> </p>
                  </li>
                  <li class="item">
                    <i class="fa fa-phone" />
                    <p>(+91) 9834567890</p>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
        <hr>
        <div class="footer-bottom ">
          <div class="row mtb-30">
            <div class="col-lg-6 ">
              <div class="copy-right ">
                © 2019 All Rights Reserved. Design By <a href="#">Aaryaweb</a>
              </div>
            </div>
            <div class="col-lg-6 ">
              <div class="footer_social pt-xs-15 center-sm">
                <ul class="social-icon">
                  <li>
                    <div class="title">
                      Follow us on :
                    </div>
                  </li>
                  <li><a title="Facebook" class="facebook"><i class="fa fa-facebook" /></a></li>
                  <li><a title="Twitter" class="twitter"><i class="fa fa-twitter" /></a></li>
                  <li><a title="Linkedin" class="linkedin"><i class="fa fa-linkedin" /></a></li>
                  <li><a title="RSS" class="rss"><i class="fa fa-rss" /></a></li>
                  <li><a title="Pinterest" class="pinterest"><i class="fa fa-pinterest" /></a></li>
                </ul>
              </div>
            </div>
          </div>
          <hr>
          <div class="row align-center mtb-30 ">
            <div class="col-12 ">
              <div class="site-link">
                <ul>
                  <li><a href="#">About Us</a></li>
                  <li><a href="#">Contact Us</a></li>
                  <li><a href="#">Customer </a></li>
                  <li><a href="#">Service</a></li>
                  <li><a href="#">Privacy</a></li>
                  <li><a href="#">Policy </a></li>
                  <li><a href="#">Accessibility</a></li>
                  <li><a href="#">Directory </a></li>
                </ul>
              </div>
            </div>
          </div>
          <div class="row align-center">
            <div class="col-12 ">
              <div class="payment">
                <ul class="payment_icon">
                  <li class="visa">
                    <a href="#"><img src="/assets/images/pay1.png" alt="Stylexpo"></a>
                  </li>
                  <li class="discover">
                    <a href="#"><img src="/assets/images/pay2.png" alt="Stylexpo"></a>
                  </li>
                  <li class="paypal">
                    <a href="#"><img src="/assets/images/pay3.png" alt="Stylexpo"></a>
                  </li>
                  <li class="vindicia">
                    <a href="#"><img src="/assets/images/pay4.png" alt="Stylexpo"></a>
                  </li>
                  <li class="atos">
                    <a href="#"><img src="/assets/images/pay5.png" alt="Stylexpo"></a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import { currentStoreView, localizedRoute } from '@vue-storefront/core/lib/multistore'
import CurrentPage from 'theme/mixins/currentPage'
import LanguageSwitcher from '../../LanguageSwitcher.vue'
import Newsletter from 'theme/components/core/blocks/Footer/Newsletter'
import BackToTop from 'theme/components/core/BackToTop'
import { getPathForStaticPage } from 'theme/helpers'
import config from 'config'

export default {
  mixins: [CurrentPage],
  name: 'MainFooter',
  methods: {
    goToAccount () {
      this.$bus.$emit('modal-toggle', 'modal-signup')
    },
    getLinkFor (path) {
      return localizedRoute(getPathForStaticPage(path))
    },
    toggleFooter (cat_name) {
      if (this.$refs[cat_name].style.display === 'none' || this.$refs[cat_name].style.display === '') {
        this.$refs[cat_name].style.display = 'block';
      } else {
        this.$refs[cat_name].style.display = 'none';
      }
    }

  },
  computed: {
    ...mapGetters({
      isLogged: 'user/isLoggedIn'
    }),
    multistoreEnabled () {
      return config.storeViews.multistore
    },
    getVersionInfo () {
      return `v${process.env.__APPVERSION__} ${process.env.__BUILDTIME__}`
    }
  },
  components: {
    Newsletter,
    LanguageSwitcher,
    BackToTop
  }
}
</script>
