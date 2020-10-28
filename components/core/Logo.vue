<template>
  <router-link :to="localizedRoute('/')" :title="$t('Home Page')" class="navbar-brand page-scroll">
    <img :alt="$t(defaultTitle)" src="/assets/images/logo.png">
  </router-link>
</template>

<script>
import config from 'config'
import { currentStoreView } from '@vue-storefront/core/lib/multistore'

export default {
  data () {
    const storeView = currentStoreView()
    return {
      defaultTitle: storeView.seo.defaultTitle ? storeView.seo.defaultTitle : config.seo.defaultTitle
    }
  },
  props: {
    width: {
      type: [String, Number],
      required: true
    },
    height: {
      type: [String, Number],
      required: true
    }
  }
}
</script>
