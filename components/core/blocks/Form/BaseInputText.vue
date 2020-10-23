<template>
  <input
    :id="getInputId"
    type="text"
    :min="min"
    :max="max"
    :disabled="disabled"
    :focus="autofocus"
    v-model="inputValue"
    :readonly="readonly"
    @blur="$emit('blur', $event.target.value)"
  >
</template>

<script>
import ValidationMessages from './ValidationMessages.vue'
export default {
  name: 'BaseInputText',
  components: {
    ValidationMessages
  },
  props: {
    value: {
      type: [String, Number],
      default: 0
    },
    name: {
      type: String,
      required: false,
      default: ''
    },
    min: {
      type: Number,
      default: 0
    },
    max: {
      type: Number,
      default: undefined
    },
    disabled: {
      type: Boolean,
      default: false
    },
    autofocus: {
      type: Boolean,
      default: false
    },
    validations: {
      type: Array,
      default: () => []
    },
    onlyPositive: {
      type: Boolean,
      default: false
    },
    readonly: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    getInputId () {
      return `input_${this._uid}`
    },
    inputValue: {
      get () {
        return this.value
      },
      set (value) {
        if (!this.onlyPositive) {
          this.inputValue = 1;
          this.$emit('input', value)
        } else {
          const targetValue = parseInt(value, 10)
          if (!isNaN(targetValue)) {
            this.$emit('input', targetValue !== 0 ? Math.abs(targetValue) : 1)
          }
        }
      }
    }
  }
}
</script>
