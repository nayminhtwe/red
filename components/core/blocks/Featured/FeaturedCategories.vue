<template>
  <no-ssr>
    <section class=" ptb-70">
      <div class="top-cate-bg">
        <div class="container">
          <div class="row">
            <div class="col-12">
              <div class="heading-part mb-30">
                <h2 class="main_title heading">
                  <span>Top Categories</span>
                </h2>
              </div>
            </div>
          </div>
          <div class="pro_cat">
            <div class="row">
              <div class="col-12">
                <div id="top-cat-pro" class="sell-pro align-center">
                  <carousel :items="7" :loop="true" :responsive-class="true"
                            :autoplay="false" :dots="false"
                            :nav="true" :responsive="{0:{items:2},480:{items:3},768:{items:4},1200:{items:5},1500:{items:7}}"
                  >
                    <div class="item" v-for="category in visibleCategories" :key="category.id">
                      <div class="categorie-box">
                        <div class="item-inner">
                          <div class="categorie-icon categorie3" />
                          <div class="cate-detail">
                            <a :href="category.url_path"><span>{{ category.name }}</span></a>
                          </div>
                        </div>
                      </div>
                    </div>
                  </carousel>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </no-ssr>
</template>

<script>
// import ButtonOutline from 'theme/components/theme/ButtonOutline'
import { mapGetters } from 'vuex'
import NoSSR from 'vue-no-ssr'
import SidebarMenu from '@vue-storefront/core/compatibility/components/blocks/SidebarMenu/SidebarMenu'

export default {
  mixins: [SidebarMenu],
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
    }),
    visibleCategories () {
      return this.categories.filter(category => {
        return category.product_count > 0 || category.children_count > 0
      })
    }
  }
}
</script>
