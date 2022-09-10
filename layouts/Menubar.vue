<template>
  <div>
    <div :class="['navbar-area', { 'is-sticky': isSticky }]">
      <div class="comero-nav">
        <div class="container">
          <nav class="navbar navbar-expand-md navbar-light">
            <nuxt-link class="navbar-brand" to="/">
              <img src="../assets/img/logo.png" alt="logo" />
            </nuxt-link>

            <b-navbar-toggle target="navbarSupportedContent"></b-navbar-toggle>

            <b-collapse
              class="collapse navbar-collapse"
              id="navbarSupportedContent"
              is-nav
            >
              <ul class="navbar-nav">
                <li class="nav-item p-relative">
                  <a href="#" class="nav-link">
                    Arrivals
                    <i class="fas fa-chevron-down"></i>
                  </a>
                  <ul class="dropdown-menu">
                    <li class="nav-item">
                      <nuxt-link to="/products-men" class="nav-link active">
                        Mens
                      </nuxt-link>
                    </li>
                    <li class="nav-item">
                      <nuxt-link to="/products-women" class="nav-link active">
                        Womens
                      </nuxt-link>
                    </li>
                    
                  </ul>
                </li>

                <li class="nav-item p-relative">
                  <a href="#" class="nav-link">
                    Shop
                    <i class="fas fa-chevron-down"></i>
                  </a>
                  <ul class="dropdown-menu">
                    <li class="nav-item">
                      <nuxt-link to="/products" class="nav-link">
                        Products
                      </nuxt-link>
                    </li>

                    <li class="nav-item">
                      <nuxt-link to="/products-details/1" class="nav-link">
                        Sport Products
                      </nuxt-link>
                    </li>
                  </ul>
                </li>

                <li class="nav-item">
                  <nuxt-link to="/gallery-one" class="nav-link">
                    Gallery
                  </nuxt-link>
                </li>

                <li class="nav-item p-relative">
                  <a href="#" class="nav-link">
                    Acessories
                    <i class="fas fa-chevron-down"></i>
                  </a>
                  <ul class="dropdown-menu">
                    <li class="nav-item">
                      <nuxt-link to="/products-sport" class="nav-link">
                        Sport
                      </nuxt-link>
                    </li>

                    <li class="nav-item">
                      <nuxt-link to="/products-shoes" class="nav-link">
                        Shoes
                      </nuxt-link>
                    </li>

                    <li class="nav-item">
                      <nuxt-link to="/products-bags" class="nav-link">
                        Bags
                      </nuxt-link>
                    </li>

                    <li class="nav-item">
                      <nuxt-link to="/products-watches" class="nav-link">
                        Watches
                      </nuxt-link>
                    </li>
                  </ul>
                </li>

                <!-- <li class="nav-item p-relative">
                  <a href="#" class="nav-link">
                    Blog
                    <i class="fas fa-chevron-down"></i>
                  </a>
                  <ul class="dropdown-menu">
                    <li class="nav-item">
                      <nuxt-link to="/blog-one" class="nav-link">
                        Blog Grid
                      </nuxt-link>
                    </li>

                    <li class="nav-item">
                      <nuxt-link to="/blog-details" class="nav-link">
                        Blog Details
                      </nuxt-link>
                    </li>
                  </ul>
                </li> -->

                <li class="nav-item">
                  <nuxt-link to="/contact" class="nav-link">
                    Contact
                  </nuxt-link>
                </li>
              </ul>

              <div class="others-option">
                <div v-if="!$store.state.authUser" class="option-item">
                  <nuxt-link to="/login">Login</nuxt-link>
                </div>
                <div v-else @click="logout" class="option-item">
                  <nuxt-link to="#">Logout</nuxt-link>
                </div>
                <div class="option-item">
                  <a @click.prevent="toggle" href="#">
                    Cart({{ cart.length }}) <i class="fas fa-shopping-bag"></i>
                  </a>
                </div>
              </div>
            </b-collapse>
          </nav>
        </div>
      </div>
    </div>

    <SidebarPanel></SidebarPanel>
  </div>
</template>

<script>
import SidebarPanel from '../layouts/SidebarPanel'
import { mutations } from '../utils/sidebar-util'

export default {
  components: {
    SidebarPanel,
  },
  data() {
    return {
      isSticky: false,
    }
  },
  mounted() {
    const that = this
    window.addEventListener('scroll', () => {
      let scrollPos = window.scrollY
      if (scrollPos >= 100) {
        that.isSticky = true
      } else {
        that.isSticky = false
      }
    })
  },
  computed: {
    cart() {
      return this.$store.getters.cart
    },
  },
  methods: {
    toggle() {
      mutations.toggleNav()
    },
    async logout(e) {
      e.preventDefault()
      try {
        await this.$store.dispatch('logout')
        this.$router.push('/')
      } catch (error) {
        this.formError = error.message
      }
    },
  },
}
</script>