<template>
  <div id="cat" class="cat-dropdown" v-if="show">
    <div class="sidebar-contant">
      <div id="menu" class="navbar-collapse collapse menu-open">
        <div class="top-right-link mobile right-side">
          <ul v-if="!currentUser">
            <li class="login-icon content">
              <a class="content-link" @click.prevent="toggleMenu('signup')">
                <span class="content-icon" />
              </a>
              <a href="#" title="Login" @click.prevent="gotoAccount('login')">Login</a> or
              <a href="#" title="Register" @click.prevent="gotoAccount('register')">Register</a>
              <div class="content-dropdown" ref="signup">
                <ul>
                  <li class="login-icon">
                    <a href="#" title="Login" @click.prevent="gotoAccount('login')"><i class="fa fa-user" /> Login</a>
                  </li>
                  <li class="register-icon">
                    <a href="#" title="Register" @click.prevent="gotoAccount('register')"><i class="fa fa-user-plus" /> Register</a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="track-icon">
              <a href="" title="Track your order"><span /> Track your order</a>
            </li>
            <li class="gift-icon">
              <a href="" title="Gift card"><span /> Gift card</a>
            </li>
          </ul>
          <ul v-else>
            <li class="login-icon content">
              <a class="content-link">
                <span class="content-icon" @click.prevent="toggleMenu('account')" />
              </a>
              <a href="#" title="Log out" @click.prevent="logout">Log out</a>
              <div class="content-dropdown" ref="account">
                <ul>
                  <li class="login-icon">
                    <a href="#" title="Log out" @click.prevent="logout"><i class="fa fa-user" /> Log out</a>
                  </li>
                  <li class="login-icon">
                    <router-link :to="localizedRoute('/my-account/orders')" :title="$t('My orders')">
                      <i class="fa fa-user-plus" />Account
                    </router-link>
                  </li>
                </ul>
              </div>
            </li>
            <li class="track-icon">
              <router-link :to="localizedRoute('/my-account/orders')" :title="$t('My orders')">
                <span /> Track your order
              </router-link>
            </li>
            <li class="gift-icon">
              <a href="" title="Gift card"><span /> Gift card</a>
            </li>
          </ul>
          <!-- <ul>
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
          </ul> -->
        </div>
        <ul class="nav navbar-nav ">
          <li class="level"
              v-for="category in categories" :key="category.slug"
              :class="category.children_count > 0 ? 'sub-megamenu': '' "
          >
            <span class="opener plus" v-if="category.children_count > 0" @click="toggleCategory(category.name)" />
            <router-link
              :to="'/'+category.url_path"
              data-testid="category.url_path"
              class="page-scroll"
            >
              <i class="fa fa-female" />{{ $t(category.name) }}
            </router-link>
            <div class="megamenu mobile-sub-menu " style="215px" v-if="category.children_count > 0" :ref="category.name">
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
        <div class="header-top mobile">
          <div class="">
            <div class="row">
              <div class="col-12">
                <div class="top-link top-link-left select-dropdown ">
                  <fieldset>
                    <button name="speed" class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all"
                            style="width: 82px;padding: 10px 5px;" @click="changeLanguage('en-US')"
                    >
                      English
                    </button>
                    <button name="speed" class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all"
                            style="width: 82px;padding: 10px 5px;" @click="changeLanguage('mm-MM')"
                    >
                      Myanmar
                    </button>
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
    },
    toggleCategory (cat_name) {
      if (this.$refs[cat_name][0].style.display === 'none' || this.$refs[cat_name][0].style.display === '') {
        this.$refs[cat_name][0].style.display = 'block';
      } else {
        this.$refs[cat_name][0].style.display = 'none';
      }
    },
    toggleMenu (cat_name) {
      if (this.$refs[cat_name].style.display === 'none' || this.$refs[cat_name].style.display === '') {
        this.$refs[cat_name].style.display = 'block';
      } else {
        this.$refs[cat_name].style.display = 'none';
      }
    },
    gotoAccount (params) {
      this.$store.commit('ui/setAuthElem', params)
      this.$bus.$emit('modal-toggle', 'modal-signup')
    },
    logout () {
      this.$bus.$emit('user-before-logout')
      this.$router.push(this.localizedRoute('/'))
    },
    changeLanguage (lang) {
      this.$i18n.locale = lang;
    }
  }
}
</script>
