<template>
  <div>
    <a class="close-cart" style="position: absoulte"
       @click.prevent="$emit('click')" v-if="component == 'header'"
    >
      <i class="fa fa-times-circle" />
    </a>
    <a class="close-cart"
       @click.prevent="$emit('click')" v-if="component == 'microcart'"
    >
      <i class="fa fa-times-circle" />
    </a>
  </div>
</template>

<script>
export default {
  props: {
    component: {
      type: String,
      required: true
    }
  }
}
</script>
