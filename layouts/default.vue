<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer" dark class="primary"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar dark
      :clipped-left="clipped"
      class="primary elevation-0 " :class="{'navbar' : $vuetify.breakpoint.mdAndUp}"
      fixed
      app
    >
      <v-app-bar-nav-icon
        class="hidden-md-and-up"
        @click.stop="drawer = !drawer"
      />
      <nuxt-link to="/">
        <img src="../static/assets/logo.png" alt="" />
      </nuxt-link>
      <v-spacer />
      <v-btn text to="/login" dark> Login </v-btn>
      <v-btn text dark> Need Help? </v-btn>
    </v-app-bar>
    <v-main class="myapp">
      <!-- <v-container> -->
      <nuxt />
      <!-- </v-container> -->
    </v-main>

    <v-footer height="400" class="pa-0" >
      <div class="footer-top pt-16" :class="{'pa-2' : $vuetify.breakpoint.smAndDown}">
        <v-container>
          <v-layout row wrap>
            <v-flex md3>
              <nuxt-link to="/">
                <img src="../static/assets/logo.png" alt="" />
              </nuxt-link>
            </v-flex>
            <v-flex md3>
              <p class="white--text font-weight-bold">Quick Links</p>
              <nuxt-link to="/" class="white--text"> Home </nuxt-link><br />
              <nuxt-link to="/" class="white--text"> About Us </nuxt-link><br />
              <nuxt-link to="/" class="white--text">
                Terms & Condition </nuxt-link
              ><br />
              <nuxt-link to="/" class="white--text"> Privacy Policy </nuxt-link>
            </v-flex>
            <v-flex md3>
              <p class="white--text font-weight-bold">How It Works</p>
              <nuxt-link to="/" class="white--text"> FAQ </nuxt-link><br />
              <nuxt-link to="/" class="white--text"> Shop </nuxt-link><br />
              <nuxt-link to="/" class="white--text"> Products </nuxt-link><br />
              <nuxt-link to="/" class="white--text"> Merchants </nuxt-link
              ><br />
              <nuxt-link to="/" class="white--text"> Others </nuxt-link>
            </v-flex>
            <v-flex md3>
              <p class="white--text font-weight-bold">Get in touch</p>
              <p class="white--text">Email: support@9pay.com.ng</p>
              <p class="white--text">Phone: +234 813 150 2944</p>
              <v-btn icon outlined color="white">
                <v-icon small>fab fa-facebook-f</v-icon>
              </v-btn>
              <v-btn icon outlined color="white">
                <v-icon small>fab fa-twitter</v-icon>
              </v-btn>
              <v-btn icon outlined color="white">
                <v-icon small>fab fa-instagram</v-icon>
              </v-btn>
              <v-btn icon outlined color="white">
                <v-icon small>fab fa-youtube</v-icon>
              </v-btn>
            </v-flex>
          </v-layout>
        </v-container>
      </div>
      <div class="footer-bottom pt-6">
        <p class="footer-text">
          &copy; {{ new Date().getFullYear() }} 9PAY | ALL RIGHTS RESERVED.
        </p>
      </div>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'home',
          title: 'Home',
          to: '/',
        },
        {
          icon: 'power_settings_new',
          title: 'Login',
          to: '/login',
        },
        {
          icon: 'how_to_reg',
          title: 'Sign Up',
          to: '#',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
    }
  },
}
</script>
<style lang="scss" scoped>
.navbar {
  padding-left: 8%;
  padding-right: 8%;
}
.myapp {
  background: #eaecef;
}

.footer-bottom {
  background: #000;
  width: 100%;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  .footer-text {
    color: #fff;
    font-size: 12px;
  }
}
.footer-top {
  background-color: #37444e;
  width: 100%;
  height: 340px;
  a {
    text-decoration: none;
  }
}

@media only screen and (max-width: 600px){
  .footer-top{
    height: auto;
  }
}
</style>
