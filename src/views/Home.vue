<template>
    <div class="home">
        <h2 class="home__header">{{header}}</h2>
        <img class="home__gif" src="../img/shrek.gif" alt="Приветственная гифка"/>
        <button @click="logOut" class="home__btn">Выйти</button>
    </div>
</template>

<script>

export default {
    name: "Home",
    data() {
        return {
            header: 'Привет, ' + localStorage.name
        }
    },
    methods: {
        logOut() {
            localStorage.name = ''
            this.$router.push('/')
        }
    }
}
</script>

<style scoped>
.home {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
}

.home__header {
    text-align: center;
    margin: 0;
    margin-bottom: 30px;
    color: #103a70;
    font-family: 'Roboto', sans-serif;
    font-weight: 700;
    font-size: 30px;
}

.home__gif {
    display: block;
    width: 500px;
    height: auto;
}

.home__btn {
  background-color: #63ABFF;
  border: none;
  border-radius: 15px;

  font-family: 'Roboto', sans-serif;
  font-weight: 500;
  font-size: 18px;
  text-transform: uppercase;
  color: #f4fafd;

  padding: 10px 20px;
  margin: 0 auto;
  margin-top: 30px;

  transition: background-color .2s linear;
}

.home__btn:hover {
  background-color: #86bfff;
  color: #f4fafd;
}
</style>