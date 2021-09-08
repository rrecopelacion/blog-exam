<template>
  <div>
    <header class="l-header">
      <div class="l-container flex flex-space-around flex-align-center">
        <h1 class="header-logo">
          <nuxt-link to="/">
            <img
            class="img-responsive"
            src="~/assets/images/site-logo.png"
            alt="site logo" />
          </nuxt-link>
        </h1>
        <nav class="header-nav">
          <ul>
            <li>
              <a
              v-if="!user"
              class="header-nav-link"
              @click.prevent="handleFormDisplay"
              href="/">{{showLoginForm || showRegisterForm ? 'CLOSE' : 'LOGIN'}}</a>

              <a
              v-else
              class="header-nav-link"
              @click.prevent="handleLogout"
              href="/">Logout</a>
            </li>
          </ul>
        </nav>
      </div>
    </header>
    <Login v-show="showLoginForm" @switch-form="handleSwitchForm" />
    <Register v-show="showRegisterForm" @switch-form="handleSwitchForm" />
  </div>
</template>

<script>
import {mapGetters, mapActions, mapMutations} from 'vuex';
import Login from './forms/Login';
import Register from './forms/Register';

export default {
  name: 'Header',
  components: {
    Login,
    Register,
  },
  methods: {
    ...mapActions('auth', ['updateLoginForm', 'updateRegisterForm', 'userLogout']),
    ...mapMutations('auth', ['setErrors']),
    handleSwitchForm(switchTo) {
    if(switchTo === 'register') {
      this.setErrors([]);
      this.updateLoginForm(false);
      setTimeout(() => {
        this.updateRegisterForm(true);
      }, 500);

    } else {
      this.updateRegisterForm(false);
      setTimeout(() => {
        this.updateLoginForm(true);
      }, 500);
    }
    },
    handleFormDisplay() {
      if(!this.showRegisterForm) {
        this.updateLoginForm(!this.showLoginForm);
      } else {
        this.updateRegisterForm(false);
      }
    },
    handleLogout() {
      localStorage.removeItem('userData');
      this.userLogout();
      this.$router.push('/');
    },
    handleDisableScroll() {
      let bodyElement = document.body.classList;
      this.showLoginForm || this.showRegisterForm
        ? bodyElement.add('is-scroll-disabled')
        : bodyElement.remove('is-scroll-disabled');
    },
  },
  computed: mapGetters('auth', ['user', 'showLoginForm', 'showRegisterForm']),
  watch: {
    showLoginForm: {
      handler: 'handleDisableScroll',
    },
    showRegisterForm: {
      handler: 'handleDisableScroll',
    },
  }
}
</script>

<style scoped lang="scss" src="./Header.scss">
