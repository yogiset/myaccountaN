<template>
<div>
    <client-only>
      <Navbar v-if="showNavbar" />
    </client-only>
    <client-only>
      <Loginbar v-if="showLoginbar" />
    </client-only>
<nuxt/>
</div>
</template>
<script>
import Navbar from '~/components/Navbar.vue'
import Loginbar from '~/components/Loginbar.vue'
export default {
components: {
Navbar,
Loginbar,
},
computed: {
    showNavbar() {
      // List of pages where you want to show the Navbar
      const pagesToShowNavbar = ['/', '/register', '/login','/forgotPassword'];
      return pagesToShowNavbar.includes(this.$route.path);
    },
    showLoginbar() {
      // List of pages where you want to show the Navbar
      const pagesToLoginbar = ['/profile','/changePassword',];
      return pagesToLoginbar.includes(this.$route.path);
    },
},


}
</script>