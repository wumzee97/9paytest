<template>
  <div style="height: 100vh">
    <v-container fill-height>
      <v-layout row wrap justify-center align-center>
        <v-flex md4>
          <v-card class="pa-8" style="z-index: 1">
            <div class="text-center">
              <nuxt-link to="/">
                <img src="../static/assets/logo.png" alt="" />
              </nuxt-link>
            </div>
            <v-form @submit.prevent="login()" lazy-validation v-model="valid" ref="login" class="mt-6">
              <h3 class="mb-2">Login to your account</h3>
              <v-text-field
                label="Username or Email"
                required
                :rules="[(v) => !!v || 'Username is required']"
                outlined v-model="username"
                dense
              >
              </v-text-field>
              <v-text-field
                label="Password"
                type="password"
                required
                :rules="[(v) => !!v || 'Password is required']"
                outlined v-model="password"
                dense
              >
              </v-text-field>
              <v-btn :loading="loading" @click="$refs.login.validate() ? login() : null" class="primary" block text>Login</v-btn>
              <div class="text-center mt-2">
                <small>
                  No account yet? <nuxt-link to="#">Sign Up</nuxt-link>
                </small>

              </div>
            </v-form>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>
<script>
export default {
  layout: 'login',
  data () {
    return {
      valid: true,
      loading: false,
      username: '',
      password: ''
    }
  },
  methods: {
    login() {
      this.loading = true
      setTimeout(() => {
        this.$router.push('/')
      }, 3000)
    }
  }
}
</script>
