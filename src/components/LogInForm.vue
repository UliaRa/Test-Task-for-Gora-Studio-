<template>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
  <div class="auth-form">
      <div class="tabs">
        <ul class="tabs__list">
            <span class="tabs__item" v-bind:class="{tabs__item_active: selectedTab === tab}" v-for="(tab, index) in tabs" :key="index" @click="selectedTab = tab">{{ tab }}</span>
        </ul>
      </div>
    <FieldsForm v-bind:logType="selectedTab === 'Email' ? 'email' : 'phone'"/>

  </div>
</template>

<script>
import FieldsForm from '@/components/FieldsForm.vue'
export default {
  components: {
    FieldsForm
  },
  data() {
    return {
      tabs: ['Email', 'Phone'],
      selectedTab: 'Email'
    }
  }
}
</script>

<style scoped>
.auth-form { 
    border-radius: 10px;  
    max-width: 500px;
    margin: 0 auto;
    background-color: rgba(224, 241, 253, 0.7);
    padding: 20px;
}

.tabs__list {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 0;
}

.tabs__item {
  padding: 0 60px;
  color: #285897;
  font-family: 'Roboto', sans-serif;
  font-weight: 500;
  font-size: 14px;
  text-transform: uppercase;

  transition: color .2s linear;
}

.tabs__item:hover {
  color: #94bef5;
}

.tabs__item_active {
  text-decoration: underline #285897 2px;

  transition: text-decoration .2s linear;
}

.tabs__item_active:hover {
  text-decoration: underline #94bef5 2px;
}
</style>