<template>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
  <div class="main">
    <h2 class="main__header">Авторизация</h2>
    <LogInForm/>
  </div>
</template>

<script>

import LogInForm from '@/components/LogInForm.vue'
export default {
  components: {
    LogInForm
  }
}
</script>

<style scoped>

.main {
  padding: 20px;
}

.main__header {
  text-align: center;
  margin: 0;
  margin-bottom: 30px;
  color: #285897;
  font-family: 'Roboto', sans-serif;
  font-weight: 700;
  font-size: 30px;
}

</style>
