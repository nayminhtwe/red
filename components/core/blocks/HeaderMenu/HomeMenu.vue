<template>
  <div id="cat" class="cat-dropdown" v-if="show">
    <div class="sidebar-contant">
      <div id="menu" class="navbar-collapse collapse">
        <div class="top-right-link mobile right-side">
          <ul>
            <li class="login-icon content">
              <a class="content-link">
                <span class="content-icon" />
              </a>
              <a href="login.html" title="Login">Login</a> or
              <a href="register.html" title="Register">Register</a>
              <div class="content-dropdown">
                <ul>
                  <li class="login-icon">
                    <a href="login.html" title="Login"><i class="fa fa-user" /> Login</a>
                  </li>
                  <li class="register-icon">
                    <a href="register.html" title="Register"><i class="fa fa-user-plus" /> Register</a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="track-icon">
              <a title="Track your order"><span /> Track your order</a>
            </li>
            <li class="gift-icon">
              <a href="" title="Gift card"><span /> Gift card</a>
            </li>
          </ul>
        </div>
        <ul class="nav navbar-nav ">
          <li class="level"
              v-for="category in visibleCategories" :key="category.slug"
              :class="category.children_count > 0 ? 'sub-megamenu': '' "
          >
            <span class="opener plus" />
            <a href="shop.html" class="page-scroll"><i class="fa fa-female" />{{ category.name }}</a>
            <div class="megamenu mobile-sub-menu " style="width:430px;" v-if="category.children_count > 0 ">
              <div class="megamenu-inner-top">
                <sub-category
                  :category-links="category.children_data"
                  :id="category.id"
                  :parent-slug="category.slug"
                  :parent-path="category.url_path"
                  v-if="category.children_count > 0"
                />
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
    <!-- <li class="level">
            <a href="shop.html" class="page-scroll"><i class="fa fa-camera-retro" />Cameras</a>
          </li>
          <li class="level sub-megamenu ">
            <span class="opener plus" />
            <a href="shop.html" class="page-scroll"><i class="fa fa-tablet" />Smartphones</a>
            <div class="megamenu mobile-sub-menu" style="width:630px;">
              <div class="megamenu-inner-top">
                <ul class="sub-menu-level1">
                  <li class="level2">
                    <a href="shop.html"><span>Women Clothings</span></a>
                    <ul class="sub-menu-level2">
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Dresses</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Sport Jeans</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Skirts</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Tops</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Sleepwear</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Jeans</a>
                      </li>
                    </ul>
                  </li>
                  <li class="level2">
                    <a href="shop.html"><span>Men Clothings</span></a>
                    <ul class="sub-menu-level2 ">
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Blazer & Coat</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Sport Shoes</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Phone Cases</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Trousers</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Purse</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Wallets</a>
                      </li>
                    </ul>
                  </li>
                  <li class="level2">
                    <a href="shop.html"><span>Juniors kid</span></a>
                    <ul class="sub-menu-level2 ">
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Blazer & Coat</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Sport Shoes</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Phone Cases</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Trousers</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Purse</a>
                      </li>
                      <li class="level3">
                        <a href="shop.html"><span>■</span>Wallets</a>
                      </li>
                    </ul>
                  </li>
                </ul>
              </div>
            </div>
          </li> -->
    </ul>
    <div class="header-top mobile">
      <div class="">
        <div class="row">
          <div class="col-12">
            <div class="top-link top-link-left select-dropdown ">
              <fieldset>
                <select name="speed" class="country option-drop">
                  <option selected="selected">
                    English
                  </option>
                  <option>Frence</option>
                  <option>German</option>
                </select>
                <select name="speed" class="currency option-drop">
                  <option selected="selected">
                    USD
                  </option>
                  <option>EURO</option>
                  <option>POUND</option>
                </select>
              </fieldset>
            </div>
          </div>
          <div class="col-12">
            <div class="top-link right-side">
              <div class="help-num">
                Need Help? : 03 233 455 55
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  </div>
  </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import i18n from '@vue-storefront/i18n'
import SidebarMenu from '@vue-storefront/core/compatibility/components/blocks/SidebarMenu/SidebarMenu'
// import SubBtn from 'theme/components/core/blocks/SidebarMenu/SubBtn'
import SubCategory from 'theme/components/core/blocks/HeaderMenu/SubCategory'
import { formatCategoryLink } from '@vue-storefront/core/modules/url/helpers'
import { disableBodyScroll, clearAllBodyScrollLocks } from 'body-scroll-lock'

export default {
  name: 'HomeMenu',
  components: {
    SubCategory
    // SubBtn
  },
  mixins: [SidebarMenu],
  props: {
    show: {
      required: true,
      type: Boolean
    }
  },
  computed: {
    mainListStyles () {
      return this.submenu.depth ? `transform: translateX(${this.submenu.depth * 100}%)` : false
    },
    ...mapState({
      submenu: state => state.ui.submenu,
      currentUser: state => state.user.current
    }),
    getSubmenu () {
      return this.submenu
    },
    visibleCategories () {
      return this.categories.filter(category => {
        return category.product_count > 0 || category.children_count > 0
      })
    },
    isCurrentMenuShowed () {
      return !this.getSubmenu || !this.getSubmenu.depth
    }
  },
  mounted () {
    this.$nextTick(() => {
      this.componentLoaded = true;
    })
  },
  destroyed () {
  },
  methods: {
    login () {
      if (!this.currentUser && this.isCurrentMenuShowed) {
        this.$nextTick(() => {
          this.$store.commit('ui/setAuthElem', 'login')
          this.$bus.$emit('modal-show', 'modal-signup')
          this.$router.push({ name: 'my-account' })
        })
      }
    },
    categoryLink (category) {
      return formatCategoryLink(category)
    }
  }
}
</script>
