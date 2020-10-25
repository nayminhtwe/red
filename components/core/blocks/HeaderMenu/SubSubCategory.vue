<template>
  <!-- <ul class="sub-menu-level2">
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
  </ul> -->
  <ul data-v-7eb379fa="" class="sub-menu-level2">
    <li data-v-7eb379fa="" class="level3">
      <a data-v-7eb379fa="" href="shop.html"><span data-v-7eb379fa="">■</span>Core i3</a> <div data-v-7eb379fa="">
        <!-- <ul data-v-7eb379fa="" class="sub-menu-level3">
          <li data-v-7eb379fa="" class="level4">
            <a data-v-7eb379fa="" href="shop.html"><span data-v-7eb379fa="">Acer</span></a> <div data-v-7eb379fa="" />
          </li>
        </ul><ul data-v-7eb379fa="" class="sub-menu-level3">
          <li data-v-7eb379fa="" class="level4">
            <a data-v-7eb379fa="" href="shop.html"><span data-v-7eb379fa="">HP</span></a> <div data-v-7eb379fa="" />
          </li>
        </ul><ul data-v-7eb379fa="" class="sub-menu-level3">
          <li data-v-7eb379fa="" class="level4">
            <a data-v-7eb379fa="" href="shop.html"><span data-v-7eb379fa="">Dell</span></a> <div data-v-7eb379fa="" />
          </li>
        </ul> -->
      </div>
    </li>
  </ul>
</template>
<script>
import { mapState } from 'vuex'
// import SubBtn from './SubBtn.vue'
import i18n from '@vue-storefront/i18n'
import config from 'config'
import { formatCategoryLink } from '@vue-storefront/core/modules/url/helpers'

export default {
  name: 'SubSubCategory',
  components: {
    // SubBtn
  },
  props: {
    id: {
      type: [String, Number],
      required: true
    },
    categoryLinks: {
      type: null,
      required: false,
      default: false
    },
    parentSlug: {
      type: String,
      required: false,
      default: ''
    },
    parentPath: {
      type: String,
      required: false,
      default: ''
    },
    myAccountLinks: {
      type: null,
      required: false,
      default: false
    }
  },
  computed: {
    children () {
      if (!config.entities.category.categoriesDynamicPrefetch && (this.categoryLinks && this.categoryLinks.length > 0 && this.categoryLinks[0].name)) { // we're using dynamic prefetching and getting just category.children_data.id from 1.7
        return this.categoryLinks
      } else {
        return this.$store.getters['category-next/getMenuCategories'].filter(c => { return c.parent_id === this.id }) // return my child categories
      }
    },
    hasChildren () {
      return this.children && this.children.length
    },
    ...mapState({
      submenu: state => state.ui.submenu,
      path: state => state.ui.submenu.path
    }),
    getSubmenu () {
      return this.submenu
    },
    styles () {
      const pos = this.submenu.path.indexOf(this.id)
      return pos !== -1 ? {
        zIndex: pos + 1
      } : false
    },
    isCurrentMenuShowed () {
      return this.getSubmenu && this.getSubmenu.depth && this.getSubmenu.path[this.getSubmenu.depth - 1] === this.id
    }
  },
  methods: {
    async logout () {
      await this.$store.dispatch('user/logout', {})
      this.$router.push(this.localizedRoute('/'))
      this.$store.commit('ui/setSubmenu', { depth: false })
    },
    notify (title) {
      if (title === 'My loyalty card' || title === 'My product reviews') {
        this.$store.dispatch('notification/spawnNotification', {
          type: 'warning',
          message: i18n.t('This feature is not implemented yet! Please take a look at https://github.com/DivanteLtd/vue-storefront/issues for our Roadmap!'),
          action1: { label: i18n.t('OK') }
        })
      }
    },
    categoryLink (category) {
      return formatCategoryLink(category)
    }
  }
}
</script>

<style scoped>
  .sidebar-submenu {
    left: 0;
    top: 0;
    min-height: 100%;
    transform: translateX(-100%);
  }

  .subcategory-item {
    display: flex;
    width: 100%;
  }
</style>
