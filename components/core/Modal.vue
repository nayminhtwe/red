<template>
  <div class="mfp-wrap mfp-close-btn-in mfp-auto-cursor mfp-ready"
       tabindex="-1" style="overflow: hidden auto;"
       data-testid="sidebar"
       v-if="isVisible"
       ref="modal"
  >
    <div class="mfp-container mfp-s-ready mfp-inline-holder">
      <div class="mfp-content" :style="style">
        <div id="account_popup" class="white-popup-block popup-position">
          <div class="popup-title" v-if="$slots.header">
            <slot name="header" />
          </div>
          <div class="popup-detail" v-if="$slots.content">
            <slot name="content" />
          </div>
          <button title="Close (Esc)" type="button" class="mfp-close" @click="close"
                  data-testid="closeModalButton" slot="close"
          >
            ×
          </button>
          <slot />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapMutations } from 'vuex'
import onEscapePress from '@vue-storefront/core/mixins/onEscapePress'
import { disableBodyScroll, clearAllBodyScrollLocks } from 'body-scroll-lock'

export default {
  name: 'Modal',
  data () {
    return {
      isVisible: false
    }
  },
  watch: {
    isVisible (state) {
      if (state) {
        this.$nextTick(() => {
          disableBodyScroll(this.$refs['modal']);
        })
      } else {
        clearAllBodyScrollLocks();
      }
    }
  },
  methods: {
    onHide (name, state, params) {
      return name === this.name ? this.toggle(false) : false
    },
    onShow (name, state, params) {
      return name === this.name ? this.toggle(true) : false
    },
    onToggle (name, state, params) {
      if (name === this.name) {
        state = typeof state === 'undefined' ? !this.isVisible : state
        this.toggle(state)
      }
    },
    onEscapePress () {
      this.close()
    },
    ...mapMutations('ui', [
      'setOverlay'
    ]),
    toggle (state) {
      this.isVisible = state
      state ? this.setOverlay(state) : setTimeout(() => this.setOverlay(state), this.delay)
    },
    close () {
      this.toggle(false)
    }
  },
  beforeMount () {
    this.$bus.$on('modal-toggle', this.onToggle)
    this.$bus.$on('modal-show', this.onShow)
    this.$bus.$on('modal-hide', this.onHide)
  },
  beforeDestroy () {
    this.$bus.$off('modal-toggle', this.onToggle)
    this.$bus.$off('modal-show', this.onShow)
    this.$bus.$off('modal-hide', this.onHide)
  },
  mixins: [onEscapePress],
  props: {
    name: {
      required: true,
      type: String
    }
  },

}
</script>