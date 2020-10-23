<template>
  <!-- <div class="product-qty">
    <label for="qty">Qty:</label>
    <div class="custom-qty">
      <button @click="value > 1 ? value-- : 1" class="reduced items" type="button">
        <i class="fa fa-minus" />
      </button> -->
  <base-input-text
    class="input-text qty"
    :name="name"
    :value="value"
    :min="1"
    :max="max"
    :disabled="disabled"
    @input="$emit('input', $event)"
    @blur="$v.$touch()"
    only-positive
    :readonly="readonly"
    :validations="[
      {
        condition: !$v.value.numeric || !$v.value.minValue || !$v.value.required,
        text: $t(`Quantity must be positive integer`)
      },
      {
        condition: maxQuantity && value && !$v.value.maxValue,
        text: $t('Quantity must be below {quantity}', { quantity: maxQuantity })
      }
    ]"
  />
  <!-- <button @click="value < maxQuantity ? value++ : maxQuantity" class="increase items" type="button">
        <i class="fa fa-plus" />
      </button>
    </div>
  </div> -->
</template>

<script>
import { minValue, maxValue, numeric, required } from 'vuelidate/lib/validators'
import { onlineHelper } from '@vue-storefront/core/helpers'
import BaseInputText from 'theme/components/core/blocks/Form/BaseInputText'
import Spinner from 'theme/components/core/Spinner'

export default {
  components: {
    Spinner,
    BaseInputText
  },
  props: {
    value: {
      type: [Number, String],
      required: true
    },
    showQuantity: {
      type: Boolean,
      default: false
    },
    maxQuantity: {
      type: Number,
      default: undefined
    },
    checkMaxQuantity: {
      type: Boolean,
      default: true
    },
    loading: {
      type: Boolean,
      default: false
    },
    isSimpleOrConfigurable: {
      type: Boolean,
      default: false
    },
    readonly: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    isOnline (value) {
      return onlineHelper.isOnline
    },
    max () {
      if (!this.isOnline || !this.isSimpleOrConfigurable) {
        return null
      }

      return this.maxQuantity
    },
    disabled () {
      if (!this.isOnline) {
        return false
      }
      return !this.maxQuantity && this.checkMaxQuantity && this.isSimpleOrConfigurable
    },
    name () {
      if (this.isSimpleOrConfigurable && !this.loading && this.showQuantity) {
        return this.$i18n.t(this.isOnline ? 'Quantity available' : 'Quantity available offline', { qty: this.maxQuantity })
      }
      return this.$i18n.t('Quantity')
    }
  },
  validations () {
    return {
      value: {
        minValue: minValue(1),
        maxValue: maxValue(this.max) && !this.isSimpleOrConfigurable,
        numeric,
        required
      }
    }
  },
  watch: {
    '$v.$invalid' (error) {
      this.$emit('error', error)
    }
  },
  methods: {
    input (value) {
      console.log(value);
      this.$emit('input', value)
    }
  }
}
</script>
