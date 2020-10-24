<template>
  <div class="container mt-sm-15">
    <div class="banner inner-banner1 ">
      <section class="banner-detail center-xs">
        <h1 class="banner-title">
          {{ category.name }}
        </h1>
        <div class="bread-crumb right-side float-none-xs">
          <ul>
            <li v-for="link in paths" :key="link.route_link">
              <router-link :to="link.route_link">
                {{ link.name | htmlDecode }}
              </router-link> /
            </li>
            <li>{{ current | htmlDecode }}</li>
          </ul>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import { Breadcrumbs } from '@vue-storefront/core/modules/breadcrumbs/components/Breadcrumbs.ts'

export default {
  mixins: [Breadcrumbs],
  props: {
    category: {
      required: true,
      type: Object
    }
  }
}
</script>
