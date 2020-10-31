<template>
  <header class="navbar navbar-custom container-full-sm" id="header">
    <div class="header-top">
      <div class="container">
        <div class="row">
          <div class="col-6">
            <div class="top-link top-link-left select-dropdown">
              <fieldset>
                <select name="speed" class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all" style="width: 82px;padding: 10px 5px;">
                  <option selected="selected">
                    <span class="ui-selectmenu-text">English</span>
                  </option>
                  <option>
                    <span class="ui-selectmenu-text">Frence</span>
                  </option>
                  <option>
                    <span class="ui-selectmenu-text">German</span>
                  </option>
                </select>
                <select name="speed" class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all" style="width: 82px;padding: 10px 5px;">
                  <option selected="selected" class="ui-selectmenu-text">
                    <span class="ui-selectmenu-text">USD</span>
                  </option>
                  <option class="ui-selectmenu-text">
                    <span class="ui-selectmenu-text">EURO</span>
                  </option>
                  <option class="ui-selectmenu-text">
                    <span class="ui-selectmenu-text">POUND</span>
                  </option>
                </select>
              </fieldset>
            </div>
          </div>
          <div class="col-6">
            <div class="top-right-link right-side">
              <ul v-if="!currentUser">
                <li class="login-icon content">
                  <a class="content-link">
                    <span class="content-icon" />
                  </a>
                  <a href="#" title="Login" @click.prevent="gotoAccount('login')">Login</a> or
                  <a href="#" title="Register" @click.prevent="gotoAccount('register')">Register</a>
                </li>
                <!-- <li class="track-icon">
                  <a href="" title="Track your order"><span /> Track your order</a>
                </li> -->
              </ul>
              <ul v-else>
                <li class="login-icon content">
                  <a class="content-link">
                    <span class="content-icon" />
                  </a>
                  <a href="#" title="Log out" @click.prevent="logout">Log out</a> or
                  <router-link :to="localizedRoute('/my-account')" :title="$t('My orders')">
                    My Account
                  </router-link>
                </li>
                <li class="track-icon">
                  <router-link :to="localizedRoute('/my-account/orders')" :title="$t('My orders')">
                    <span /> Track your order
                  </router-link>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="header-middle">
      <div class="container">
        <hr>
        <div class="row">
          <div class="col-xl-3 col-md-3 col-xl-20per">
            <div class="header-middle-left">
              <div class="navbar-header float-none-sm">
                <logo />
              </div>
            </div>
          </div>
          <div class="col-xl-6 col-md-6 col-xl-60per">
            <div class="header-right-part">
              <div class="main-search">
                <div class="header_search_toggle desktop-view">
                  <form>
                    <div class="search-box">
                      <input class="input-text" type="text" placeholder="Search entire store here..." v-model="keyword">
                      <button class="search-btn" @click.prevent="search" />
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-xl-3 col-md-3 col-xl-20per">
            <div class="right-side float-left-xs header-right-link">
              <ul>
                <!-- <li class="compare-icon">
                  <a href="compare.html">
                    <span />
                  </a>
                </li> -->
                <li class="wishlist-icon">
                  <router-link :to="localizedRoute('/wishlist')">
                    <span />
                  </router-link>
                </li>
                <li class="cart-icon">
                  <a> <span />
                    <div class="my-cart"
                         productsInCart
                         v-for="(segment, index) in totals"
                         :key="index" v-if="segment.code === 'grand_total'"
                    >
                      <div v-if="productsInCart.length">{{ totalQuantity }} items<br>{{ segment.value | price(storeView) }}</div>
                    </div>
                  </a>
                  <div class="cart-dropdown header-link-dropdown">
                    <ul class="cart-list link-dropdown-list">
                      <product v-for="product in productsInCart" :key="product.server_item_id || product.id" :product="product" component="header" />
                    </ul>
                    <div v-for="(segment, index) in totals" :key="index" v-if="segment.code === 'grand_total'">
                      <p class="cart-sub-totle" v-if="productsInCart.length">
                        <span class="pull-left">
                          {{ segment.title }}
                        </span>
                        <span class="pull-right">
                          <strong class="price-box">
                            {{ segment.value | price(storeView) }}
                          </strong>
                        </span>
                      </p>
                    </div>
                    <div class="clearfix" />
                    <div class="mt-20">
                      <router-link :to="{ name: 'cart' }" class="btn-color btn">
                        Cart
                      </router-link>
                      <router-link :to="{ name: 'checkout' }" class="btn-color btn right-side">
                        Checkout
                      </router-link>
                      <!-- <a href="checkout.html" class="btn-color btn right-side">Checkout</a> -->
                    </div>
                  </div>
                </li>
                <li class="side-toggle">
                  <button data-target=".navbar-collapse" data-toggle="collapse" class="navbar-toggle" type="button" @click="openCatDrop = !openCatDrop">
                    <i class="fa fa-bars" />
                  </button>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="header-bottom">
      <div class="container">
        <div class="row position-r">
          <div class="col-xl-2 col-lg-3 col-xl-20per position-s">
            <div class="sidebar-menu-dropdown home">
              <a class="btn-sidebar-menu-dropdown" @click.prevent="openCatDrop = !openCatDrop"><span /> Categories </a>
              <home-menu :show="openCatDrop" />
            </div>
          </div>
          <div class="col-xl-6 col-lg-6 col-xl-60per">
            <div class="bottom-inner">
              <div class="position-r">
                <div class="nav_sec position-r">
                  <div class="mobilemenu-title mobilemenu" @click="toggleMenu('bottomMenu')">
                    <span>Menu</span>
                    <i class="fa fa-bars pull-right" />
                  </div>
                  <div class="mobilemenu-content" ref="bottomMenu">
                    <ul class="nav navbar-nav" id="menu-main">
                      <li class="active">
                        <router-link :to="localizedRoute('/')" :title="$t('Home Page')">
                          <span>Home</span>
                        </router-link>
                      </li>
                      <li>
                        <router-link :to="localizedRoute('/about-us')" :title="$t('About us')">
                          <span>About Us</span>
                        </router-link>
                      </li>
                      <li>
                        <router-link :to="localizedRoute('/delivery')" :title="$t('Delivery')">
                          <span>Delivery</span>
                        </router-link>
                      </li>
                      <li>
                        <router-link :to="localizedRoute('/contact')" :title="$t('Contact us')">
                          <span>Contact us</span>
                        </router-link>
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-xl-4 col-lg-3 col-xl-20per d-none d-lg-block">
            <div class="right-side float-left-xs header-right-link">
              <div class="offer-btn right-side">
                <a href="#" class="gift-offer">
                  <i class="fa fa-gift" /> Offers
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="popup-links ">
      <div class="popup-links-inner">
        <ul>
          <hamburger-icon />
          <microcart-icon />
          <account-icon />
          <li class="search">
            <a class="popup-with-form" href="#search_popup"><span class="icon" /><span class="icon-text">Search</span></a>
          </li>
          <li class="scroll scrollup">
            <a href="#"><span class="icon" /><span class="icon-text">Scroll-top</span></a>
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<script>
import { mapGetters, mapState } from 'vuex'
import CurrentPage from 'theme/mixins/currentPage'
import AccountIcon from 'theme/components/core/blocks/Header/AccountIcon'
import CompareIcon from 'theme/components/core/blocks/Header/CompareIcon'
import HamburgerIcon from 'theme/components/core/blocks/Header/HamburgerIcon'
import HomeMenu from 'theme/components/core/blocks/HeaderMenu/HomeMenu'
import Logo from 'theme/components/core/Logo'
import MicrocartIcon from 'theme/components/core/blocks/Header/MicrocartIcon'
import SearchIcon from 'theme/components/core/blocks/Header/SearchIcon'
import WishlistIcon from 'theme/components/core/blocks/Header/WishlistIcon'
import Product from 'theme/components/core/blocks/Microcart/Product'
import { syncCartWhenLocalStorageChange } from '@vue-storefront/core/modules/cart/helpers'

export default {
  name: 'Header',
  components: {
    AccountIcon,
    CompareIcon,
    HamburgerIcon,
    Logo,
    MicrocartIcon,
    SearchIcon,
    WishlistIcon,
    Product,
    HomeMenu
  },
  mixins: [CurrentPage],
  data () {
    return {
      navVisible: true,
      isScrolling: false,
      scrollTop: 0,
      lastScrollTop: 0,
      navbarHeight: 64,
      openCatDrop: false,
      keyword: ''
    }
  },
  computed: {
    ...mapState({
      isOpenLogin: state => state.ui.signUp,
      currentUser: state => state.user.current
    }),
    ...mapGetters({
      productsInCart: 'cart/getCartItems',
      totals: 'cart/getTotals',
      totalQuantity: 'cart/getItemsTotalQuantity'
    }),
    isThankYouPage () {
      return this.$store.state.checkout.isThankYouPage
        ? this.$store.state.checkout.isThankYouPage
        : false
    }
  },
  beforeMount () {
    window.addEventListener(
      'scroll',
      () => {
        this.isScrolling = true
      },
      { passive: true }
    )

    setInterval(() => {
      if (this.isScrolling) {
        this.hasScrolled()
        this.isScrolling = false
      }
    }, 250)
  },
  mounted () {
    syncCartWhenLocalStorageChange.addEventListener()
    this.$once('hook:beforeDestroy', () => {
      syncCartWhenLocalStorageChange.removeEventListener()
    })
  },
  methods: {
    gotoAccount (params) {
      this.$store.commit('ui/setAuthElem', params)
      this.$bus.$emit('modal-toggle', 'modal-signup')
    },
    logout () {
      this.$bus.$emit('user-before-logout')
      this.$router.push(this.localizedRoute('/'))
    },
    Scrolled () {
      this.scrollTop = window.scrollY
      if (
        this.scrollTop > this.lastScrollTop &&
        this.scrollTop > this.navbarHeight
      ) {
        this.navVisible = false
      } else {
        this.navVisible = true
      }
      this.lastScrollTop = this.scrollTop
    },
    search () {
      this.$router.push({ name: 'search', params: { keyword: this.keyword } });
    },
    toggleMenu (cat_name) {
      if (this.$refs[cat_name].style.display === 'none' || this.$refs[cat_name].style.display === '') {
        this.$refs[cat_name].style.display = 'block';
      } else {
        this.$refs[cat_name].style.display = 'none';
      }
    }
  }
}
</script>
