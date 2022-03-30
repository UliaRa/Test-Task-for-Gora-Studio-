<template>
  <div id="app">
    <router-view :key="$route.fullPath"></router-view>
    
  </div>
</template>

<script>

export default {
  name: 'App',
  mounted() {
    if (localStorage.name) {
      this.$router.push('/home')
    }
  }
}

</script>
