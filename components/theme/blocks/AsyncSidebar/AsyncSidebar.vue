<template>
  <no-ssr>
    <div class="mfp-wrap mfp-close-btn-in mfp-auto-cursor mfp-ready"
         tabindex="-1" style="overflow: hidden auto;"
         data-testid="sidebar"
         ref="sidebar"
         v-show="isOpen"
    >
      <div class="mfp-container mfp-s-ready mfp-inline-holder">
        <div class="mfp-content">
          <component :is="component" @close="$emit('close')" @reload="getComponent" />
        </div>
      </div>
    </div>
  </no-ssr>
</template>

<script>
import NoSSR from 'vue-no-ssr'
import LoadingSpinner from 'theme/components/theme/blocks/AsyncSidebar/LoadingSpinner.vue'
import LoadingError from 'theme/components/theme/blocks/AsyncSidebar/LoadingError.vue'
import { disableBodyScroll, clearAllBodyScrollLocks } from 'body-scroll-lock'

export default {
  props: {
    asyncComponent: {
      type: Function,
      required: true
    },
    isOpen: {
      type: Boolean,
      default: false
    },
    /** "right" or "left"  */
    direction: {
      type: String,
      default: 'right'
    }
  },
  components: {
    'no-ssr': NoSSR
  },
  data () {
    return {
      component: null
    }
  },
  watch: {
    isOpen (state) {
      if (state) {
        if (!this.component) {
          this.getComponent()
        }
        // this.$nextTick(() => {
        //   disableBodyScroll(this.$refs.sidebar)
        // })
      // } else {
      //   clearAllBodyScrollLocks()
      }
    }
  },
  methods: {
    getComponent () {
      this.component = () => ({
        component: this.asyncComponent(),
        loading: LoadingSpinner,
        error: LoadingError,
        timeout: 3000
      })
    }
  }
}
</script>
