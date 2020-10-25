<template>
  <div id="account_popup" class="white-popup-block popup-position">
    <div class="popup-title">
      <h2 class="main_title heading">
        <span>{{ $t('Log in') }}</span>
      </h2>
    </div>
    <div class="popup-detail">
      <div class="row">
        <div class="col-12">
          <div class="row justify-content-center">
            <div class="col-xl-12 col-lg-8 col-md-8 ">
              <form class="main-form full" @submit.prevent="login">
                <div class="row">
                  <div class="col-12">
                    <div class="input-box">
                      <label for="login-email">Email address</label>
                      <input id="login-email" type="email" required
                             :placeholder="$t('E-mail address *')" v-model="email"
                             @blur="$v.email.$touch()"
                      >
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="input-box">
                      <label for="login-pass">Password</label>
                      <input id="login-pass" type="password" required :placeholder="$t('Password *')"
                             v-model="password" @blur="$v.password.$touch()"
                      >
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="check-box left-side">
                      <span>
                        <input type="checkbox" name="remember_me" id="remember_me" class="checkbox" v-model="remember">
                        <label for="remember_me">Remember Me</label>
                      </span>
                    </div>
                    <button name="submit" type="submit" class="btn-color right-side">
                      Log In
                    </button>
                  </div>
                  <div class="col-12">
                    <a title="Forgot Password" class="forgot-password mtb-20"
                       href="#" @click.prevent="remindPassword"
                    >
                      {{ $t('Forgot the password?') }}
                    </a>
                    <hr>
                  </div>
                  <div class="col-12">
                    <div class="new-account align-center mt-20">
                      <span>New to 21 Marts?</span>
                      <a class="link" @click.prevent="switchElem" data-testid="registerLink">
                        {{ $t('register an account') }}
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
import Login from '@vue-storefront/core/compatibility/components/blocks/Auth/Login'

import ButtonFull from 'theme/components/theme/ButtonFull.vue'
import BaseCheckbox from '../Form/BaseCheckbox.vue'
import BaseInput from '../Form/BaseInput.vue'
import { required, email } from 'vuelidate/lib/validators'

export default {
  mixins: [Login],
  validations: {
    email: {
      required,
      email
    },
    password: {
      required
    }
  },
  data () {
    return {
      hasRedirect: !!localStorage.getItem('redirect')
    }
  },
  methods: {
    close (e) {
      if (e) localStorage.removeItem('redirect')
      this.$bus.$emit('modal-hide', 'modal-signup')
    },
    login () {
      if (this.$v.$invalid) {
        this.$v.$touch()
        this.$store.dispatch('notification/spawnNotification', {
          type: 'error',
          message: this.$t('Please fix the validation errors'),
          action1: { label: this.$t('OK') }
        })
        return
      }
      this.callLogin()
    },
    remindPassword () {
      if (!(typeof navigator !== 'undefined' && navigator.onLine)) {
        this.$store.dispatch('notification/spawnNotification', {
          type: 'error',
          message: this.$t('Reset password feature does not work while offline!'),
          action1: { label: this.$t('OK') }
        })
      } else {
        this.callForgotPassword()
      }
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
  },
  components: {
    ButtonFull,
    BaseCheckbox,
    BaseInput
  }
}
</script>
