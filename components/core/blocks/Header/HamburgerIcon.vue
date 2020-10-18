<template>
  <li class="categories">
    <a class="popup-with-form" href="#"
       @click.prevent="openSidebarMenu"
       :aria-label="$t('Open menu')"
       data-testid="menuButton"
    >
      <span class="icon" />
      <span class="icon-text">Categories
      </span>
    </a>
  </li>
</template>

<script>
import HamburgerIcon from '@vue-storefront/core/compatibility/components/blocks/Header/HamburgerIcon'

export default {
  mixins: [HamburgerIcon]
}
</script>
