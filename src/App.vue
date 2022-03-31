<template>
  <div id="app">
    <TC/>
  </div>
</template>

<script>
import TC from './components/TC.vue'

export default {
  name: 'App',
  components: {
    TC
  }
}
</script>

<style lang="scss">
// Import Bulma's core
//@import "~bulma/sass/utilities/_all";
@import "assets/sass/main.scss";

</style>
