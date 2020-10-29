<template>
  <div class="sidebar-box mb-40">
    <span class="opener plus" @click="toggleBlock('filter')" />
    <div class="sidebar-title">
      <h3><span>{{ $t('Filter') }}</span></h3>
    </div>
    <div class="sidebar-contant" ref="filter">
      <div class="size mb-20" v-for="(filter, filterIndex) in availableFilters"
           :key="filterIndex"
      >
        <div class="inner-title">
          {{ $t(filterIndex + '_filter') }}
        </div>
        <div v-if="filterIndex==='color'">
          <color-selector
            context="category"
            code="color"
            v-for="(color, index) in filter"
            :key="index"
            :variant="color"
            :selected-filters="getCurrentFilters"
            @change="$emit('changeFilter', $event)"
          />
        </div>
        <div v-else-if="filterIndex==='size'">
          <size-selector
            context="category"
            code="size"
            class="size-select mr10 mb10"
            v-for="(size, index) in sortById(filter)"
            :key="index"
            :variant="size"
            :selected-filters="getCurrentFilters"
            @change="$emit('changeFilter', $event)"
          />
        </div>
        <div v-else-if="filterIndex==='price'">
          <price-selector
            context="category"
            class="price-select mb10 block"
            code="price"
            v-for="(price, index) in filter"
            :key="index"
            :id="price.id"
            :from="price.from"
            :to="price.to"
            :content="price.label"
            :variant="price"
            :selected-filters="getCurrentFilters"
            @change="$emit('changeFilter', $event)"
          />
        </div>
        <div v-else class="sidebar__inline-selecors">
          <generic-selector
            context="category"
            class="mr10 mb10 block"
            :code="filterIndex"
            v-for="(option, index) in filter"
            :key="index"
            :variant="option"
            :selected-filters="getCurrentFilters"
            @change="$emit('changeFilter', $event)"
          />
        </div>
      </div>
      <a href="#" class="btn btn-color" @click.prevent="resetAllFilters">Refine</a>
    </div>
  </div>
</template>

<script>
import ColorSelector from 'theme/components/core/ColorSelector'
import SizeSelector from 'theme/components/core/SizeSelector'
import PriceSelector from 'theme/components/core/PriceSelector'
import GenericSelector from 'theme/components/core/GenericSelector'
import pickBy from 'lodash-es/pickBy'

export default {
  components: {
    ColorSelector,
    SizeSelector,
    PriceSelector,
    GenericSelector
  },
  props: {
    filters: {
      type: Object,
      required: true
    }
  },
  computed: {
    hasActiveFilters () {
      return this.$store.getters['category-next/hasActiveFilters']
    },
    getCurrentFilters () {
      return this.$store.getters['category-next/getCurrentFilters']
    },
    availableFilters () {
      return pickBy(this.filters, (filter, filterType) => { return (filter.length && !this.$store.getters['category-next/getSystemFilterNames'].includes(filterType)) })
    }
  },
  methods: {
    resetAllFilters () {
      this.$store.dispatch('category-next/resetSearchFilters')
    },
    sortById (filters) {
      return [...filters].sort((a, b) => { return a.id - b.id })
    },
    toggleBlock (cat_name) {
      if (this.$refs[cat_name].style.display === 'none' || this.$refs[cat_name].style.display === '') {
        this.$refs[cat_name].style.display = 'block';
      } else {
        this.$refs[cat_name].style.display = 'none';
      }
    }
  }
}
</script>
