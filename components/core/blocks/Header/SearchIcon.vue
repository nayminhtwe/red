<template>
  <li class="search">
    <a class="popup-with-form" href="#"
       @click.prevent="toggleSearchpanel"
       data-testid="openSearchPanel"
       :aria-label="$t('Open search panel')"
    >
      <span class="icon" />
      <span class="icon-text">Search</span>
    </a>
  </li>
</template>

<script>
import SearchIcon from '@vue-storefront/core/compatibility/components/blocks/Header/SearchIcon'

export default {
  mixins: [SearchIcon]
}
</script>
