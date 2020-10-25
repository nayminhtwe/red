<template>
  <!-- <div id="cat" class="cat-dropdown" v-if="show">
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
            <router-link
              :to="'/'+category.url_path"
              data-testid="category.url_path"
              class="page-scroll"
            >
              <i class="fa fa-female" />{{ category.name }}
            </router-link>
            <div class="megamenu mobile-sub-menu " style="215px" v-if="category.children_count > 0 ">
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
  </div> -->
  <div id="cat" class="cat-dropdown">
    <div class="sidebar-contant">
      <div id="menu" class="navbar-collapse collapse menu-open">
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
            <span class="opener plus" v-if="category.children_count > 0" />
            <router-link
              :to="'/'+category.url_path"
              data-testid="category.url_path"
              class="page-scroll"
            >
              <i class="fa fa-female" />{{ category.name }}
            </router-link>
            <div class="megamenu mobile-sub-menu " style="215px" v-if="category.children_count > 0 ">
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
                    <select name="speed" class="country option-drop" id="ui-id-3" style="display: none;">
                      <option selected="selected">
                        English
                      </option>
                      <option>Frence</option>
                      <option>German</option>
                    </select><span class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all" tabindex="0" id="ui-id-3-button" role="combobox" aria-expanded="false" aria-autocomplete="list" aria-owns="ui-id-3-menu" aria-haspopup="true" style="width: 82px;"><span class="ui-icon ui-icon-triangle-1-s" /><span class="ui-selectmenu-text">English</span></span>
                    <select name="speed" class="currency option-drop" id="ui-id-4" style="display: none;">
                      <option selected="selected">
                        USD
                      </option>
                      <option>EURO</option>
                      <option>POUND</option>
                    </select><span class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all" tabindex="0" id="ui-id-4-button" role="combobox" aria-expanded="false" aria-autocomplete="list" aria-owns="ui-id-4-menu" aria-haspopup="true" style="width: 82px;"><span class="ui-icon ui-icon-triangle-1-s" /><span class="ui-selectmenu-text">USD</span></span>
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
    }
  }
}
</script>
