<template>
  <div id="account_popup" class="white-popup-block popup-position">
    <div class="popup-title">
      <h2 class="main_title heading">
        <span>{{ $t('Register') }}</span>
      </h2>
    </div>
    <div class="popup-detail">
      <div class="row">
        <div class="col-12">
          <div class="row justify-content-center">
            <div class="col-xl-12 col-lg-8 col-md-8 ">
              <form @submit.prevent="register" class="main-form full">
                <div class="row">
                  <div class="col-12">
                    <div class="input-box">
                      <label for="f-name">First Name</label>
                      <input type="text" id="f-name"
                             autocomplete="given-name"
                             v-model="firstName"
                             @blur="$v.firstName.$touch()"
                             :placeholder="$t('First name *')"
                      >
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="input-box">
                      <label for="l-name">Last Name</label>
                      <input type="text" id="l-name"
                             autocomplete="last-name"
                             v-model="lastName"
                             @blur="$v.lastName.$touch()"
                             :placeholder="$t('Last name *')"
                      >
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="input-box">
                      <label for="login-email">Email address</label>
                      <input id="login-email" type="email"
                             autocomplete="email"
                             v-model="email"
                             @blur="$v.email.$touch()"
                             focus
                             :placeholder="$t('E-mail address *')"
                      >
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="input-box">
                      <label for="login-pass">Password</label>
                      <input id="login-pass" type="password"
                             ref="password"
                             autocomplete="new-password"
                             v-model="password"
                             @blur="$v.password.$touch()"
                             :placeholder="$t('Password *')"
                      >
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="input-box">
                      <label for="re-enter-pass">Re-enter Password</label>
                      <input id="re-enter-pass" type="password"
                             autocomplete="new-password"
                             v-model="rPassword"
                             @blur="$v.rPassword.$touch()"
                             :placeholder="$t('Repeat password *')"
                      >
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="check-box left-side mb-20">
                      <span>
                        <input type="checkbox" name="remember_me" id="remember_me"
                               class="checkbox"
                               v-model="conditions"
                               @blur="$v.conditions.$reset()"
                               @change="$v.conditions.$touch()"
                        >
                        <label for="remember_me">{{ $t('I accept terms and conditions') }} *</label>
                      </span>
                    </div>
                    <button name="submit" type="submit" class="btn-color right-side">
                      {{ $t('Register an account') }}
                    </button>
                  </div>
                  <div class="col-12">
                    <hr>
                    <div class="new-account align-center mt-20">
                      <span>Or</span>
                      <a href="#" @click.prevent="switchElem">
                        {{ $t('login to your account') }}
                      </a>
                    </div>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
      <button title="Close (Esc)" type="button" class="mfp-close" @click="close">
        ×
      </button>
    </div>
  </div>
</template>
<script>
import Register from '@vue-storefront/core/compatibility/components/blocks/Auth/Register'
import ButtonFull from 'theme/components/theme/ButtonFull.vue'
import BaseCheckbox from 'theme/components/core/blocks/Form/BaseCheckbox.vue'
import BaseInput from 'theme/components/core/blocks/Form/BaseInput.vue'
import { required, email, minLength, sameAs, alpha } from 'vuelidate/lib/validators'

export default {
  validations: {
    email: {
      required,
      email
    },
    firstName: {
      minLength: minLength(2),
      required,
      alpha
    },
    lastName: {
      required,
      alpha
    },
    password: {
      minLength: minLength(8),
      required
    },
    rPassword: {
      required,
      sameAsPassword: sameAs('password')
    },
    conditions: {
      sameAs: sameAs(() => true)
    }
  },
  mixins: [Register],
  components: {
    ButtonFull,
    BaseCheckbox,
    BaseInput
  },
  methods: {
    register () {
      if (this.$v.$invalid) {
        this.$v.$touch()
        this.$store.dispatch('notification/spawnNotification', {
          type: 'error',
          message: this.$t('Please fix the validation errors'),
          action1: { label: this.$t('OK') }
        })
        return
      }
      this.callRegister()
    },
    onSuccess () {
      this.$store.dispatch('notification/spawnNotification', {
        type: 'success',
        message: this.$t('You are logged in!'),
        action1: { label: this.$t('OK') }
      })
    },
    onFailure (result) {
      this.$store.dispatch('notification/spawnNotification', {
        type: 'error',
        message: this.$t(result.result),
        action1: { label: this.$t('OK') }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  .modal-header{
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .modal-close{
    cursor: pointer;
  }
  .modal-content {
    @media (max-width: 400px) {
      padding-left: 20px;
      padding-right: 20px;
    }
  }
</style>
