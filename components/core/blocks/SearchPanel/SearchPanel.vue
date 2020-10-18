<template>
  <div id="search_popup" class="white-popup-block popup-position">
    <div class="popup-title">
      <h2 class="main_title heading">
        <span>Search</span>
      </h2>
    </div>
    <div class="popup-detail">
      <div class="main-search">
        <div class="header_search_toggle desktop-view">
          <form>
            <div class="search-box">
              <input class="input-text" type="text" placeholder="Search entire store here...">
              <button class="search-btn" />
            </div>
          </form>
        </div>
      </div>
    </div>
    <button title="Close (Esc)" type="button" class="mfp-close" @click="closeSearchpanel"
            data-testid="closeSearchPanel"
    >
      ×
    </button>
  </div>
</template>

<script>
import SearchPanel from '@vue-storefront/core/compatibility/components/blocks/SearchPanel/SearchPanel'
import ProductTile from 'theme/components/core/ProductTile'
import VueOfflineMixin from 'vue-offline/mixin'
import CategoryPanel from 'theme/components/core/blocks/Category/CategoryPanel'
import { minLength } from 'vuelidate/lib/validators'
import { disableBodyScroll, clearAllBodyScrollLocks } from 'body-scroll-lock'

export default {
  components: {
    ProductTile,
    CategoryPanel
  },
  mixins: [SearchPanel, VueOfflineMixin],
  validations: {
    search: {
      minLength: minLength(3)
    }
  },
  data () {
    return {
      selectedCategoryIds: []
    }
  },
  computed: {
    visibleProducts () {
      const productList = this.products || []
      if (this.selectedCategoryIds.length) {
        return productList.filter(product => product.category_ids.some(categoryId => {
          return this.selectedCategoryIds.includes(categoryId)
        }))
      }
      return productList
    },
    categories () {
      const categories = this.products
        .filter(p => p.category)
        .map(p => p.category)
        .flat()

      const distinctCategories = Array.from(
        new Set(categories.map(c => c.category_id))
      ).map(catId => categories.find(c => c.category_id === catId))

      return distinctCategories
    },
    getNoResultsMessage () {
      let msg = ''
      if (!this.$v.search.minLength) {
        msg = 'Searched term should consist of at least 3 characters.'
      } else if (this.emptyResults) {
        msg = 'No results were found.'
      }
      return msg
    }
  },
  watch: {
    categories () {
      this.selectedCategoryIds = []
    }
  },
  mounted () {
    // add autofocus to search input field
    this.$refs.search.focus()
    disableBodyScroll(this.$el)
  },
  destroyed () {
    clearAllBodyScrollLocks()
  }
}
</script>
