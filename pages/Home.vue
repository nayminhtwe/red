<template>
  <div id="home">
    <head-image />
    <featured-blocks />
    <welcome />
    <featured-categories />
    <lazy-hydrate :trigger-hydration="!loading" v-if="isLazyHydrateEnabled">
      <featured-products :products="getEverythingNewCollection" />
    </lazy-hydrate>
    <lazy-hydrate :trigger-hydration="!loading" v-if="isLazyHydrateEnabled">
      <featured-products :products="getEverythingNewCollection" />
    </lazy-hydrate>
    <lazy-hydrate :trigger-hydration="!loading" v-if="isLazyHydrateEnabled">
      <featured-products :products="getEverythingNewCollection" />
    </lazy-hydrate>
    <lazy-hydrate :trigger-hydration="!loading" v-if="isLazyHydrateEnabled">
      <countdown-products :products="getEverythingNewCollection" />
    </lazy-hydrate>
    <featured-brands />
  </div>
</template>

<script>
// query constructor
import { isServer, onlineHelper } from '@vue-storefront/core/helpers'
import LazyHydrate from 'vue-lazy-hydration'

// Theme core components
import ProductListing from 'theme/components/core/ProductListing'
import HeadImage from 'theme/components/core/blocks/MainSlider/HeadImage'
import FeaturedCategories from 'theme/components/core/blocks/Featured/FeaturedCategories'
import FeaturedBlocks from 'theme/components/core/blocks/Featured/FeaturedBlocks'
import FeaturedBrands from 'theme/components/core/blocks/Featured/FeaturedBrands'
import FeaturedProducts from 'theme/components/core/blocks/Featured/FeaturedProducts'
import Welcome from 'theme/components/core/blocks/Featured/Welcome'
import CountdownProducts from 'theme/components/core/blocks/Featured/CountdownProducts'
// Theme local components
import Onboard from 'theme/components/theme/blocks/Home/Onboard'
import PromotedOffers from 'theme/components/theme/blocks/PromotedOffers/PromotedOffers'
import TileLinks from 'theme/components/theme/blocks/TileLinks/TileLinks'
import { Logger } from '@vue-storefront/core/lib/logger'
import { mapGetters } from 'vuex'
import config from 'config'
import { registerModule } from '@vue-storefront/core/lib/modules'
import { RecentlyViewedModule } from '@vue-storefront/core/modules/recently-viewed'

export default {
  data () {
    return {
      loading: true
    }
  },
  components: {
    HeadImage,
    Onboard,
    ProductListing,
    PromotedOffers,
    TileLinks,
    LazyHydrate,
    FeaturedCategories,
    FeaturedBlocks,
    FeaturedBrands,
    FeaturedProducts,
    Welcome,
    CountdownProducts
  },
  computed: {
    ...mapGetters('user', ['isLoggedIn']),
    ...mapGetters('homepage', ['getEverythingNewCollection']),
    categories () {
      return this.getCategories
    },
    isOnline () {
      return onlineHelper.isOnline
    },
    isLazyHydrateEnabled () {
      return config.ssr.lazyHydrateFor.some(
        field => ['homepage', 'homepage.new_collection'].includes(field)
      )
    }
  },
  beforeCreate () {
    registerModule(RecentlyViewedModule)
  },
  async beforeMount () {
    if (this.$store.state.__DEMO_MODE__) {
      const onboardingClaim = await this.$store.dispatch('claims/check', { claimCode: 'onboardingAccepted' })
      if (!onboardingClaim) { // show onboarding info
        this.$bus.$emit('modal-toggle', 'modal-onboard')
        this.$store.dispatch('claims/set', { claimCode: 'onboardingAccepted', value: true })
      }
    }
  },
  mounted () {
    if (!this.isLoggedIn && localStorage.getItem('redirect')) this.$bus.$emit('modal-show', 'modal-signup')
  },
  watch: {
    isLoggedIn () {
      const redirectObj = localStorage.getItem('redirect')
      if (redirectObj) this.$router.push(redirectObj)
      localStorage.removeItem('redirect')
    }
  },
  async asyncData ({ store, route, context }) { // this is for SSR purposes to prefetch data
    if (context) context.output.cacheTags.add(`home`)
    Logger.info('Calling asyncData in Home Page (core)')()

    await Promise.all([
      store.dispatch('homepage/fetchNewCollection'),
      store.dispatch('promoted/updateHeadImage'),
      store.dispatch('promoted/updatePromotedOffers')
    ])
  },
  beforeRouteEnter (to, from, next) {
    if (!isServer && !from.name) { // Loading products to cache on SSR render
      next(vm =>
        vm.$store.dispatch('homepage/fetchNewCollection').then(res => {
          vm.loading = false
        })
      )
    } else {
      next()
    }
  },
  metaInfo () {
    return {
      title: this.$route.meta.title || this.$i18n.t('Home Page'),
      meta: this.$route.meta.description ? [{ vmid: 'description', name: 'description', content: this.$route.meta.description }] : []
    }
  }
}
</script>
