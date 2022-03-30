<template>
  <div class="auth-block">
    <InputForm v-bind:params="forms[0]" @login='setEmail'/>
    <InputForm v-bind:params="forms[1]" @login='setPass'/>
    <span v-bind:class="{auth__error: error !== ''}">{{error}}</span>
    <button type="submit" @click="logIn" class="btn_login">Войти</button>
  </div>
</template>

<script>

import InputForm from '@/components/InputForm.vue'
import crc32 from 'crc/crc32'
export default {
    components: {
        InputForm
    },
    data() {
    return {
      forms: [
        {label: "Email:", input: "email"},
        {label: "Пароль:", input: "pass"}
      ],
      email: '',
      password: '',
      users: [],
      error: ''
    }
  },
  created() {
    fetch("users.json")
      .then(r => r.json())
      .then(json => {
        this.users=json.users
      },
      response => {
        console.log('Error loading json:', response)
    });
  },
  methods: {
    logIn() {
        if (this.email !== '' && this.password !== '') {
          let cur_email = crc32(this.email).toString(16)
          let cur_pass = crc32(this.password).toString(16)
          let aim = ''
          for (let i = 0; i < this.users.length; i++) {
            if (this.users[i].email === cur_email && this.users[i].password === cur_pass) {
              aim = this.users[i]
              break
            }
          }
          if (aim === '') {
            this.error = 'Пользователь не найден'
          }
          else {
            localStorage.name = this.email
            this.$router.push('/home')
          }
        }
        else {
          this.error = 'Заполните поля'
        }
    },
    setEmail(value) {
      this.error = ''
      this.email = value
    },
    setPass(value) {
      this.error = ''
      this.password = value
    }
  }
}
</script>

<style scoped>
.auth-block {
  display: flex;
  flex-direction: column;
}

.auth__error {
    color: #FF0021;

    margin-left: 10px;
    margin-top: 5px;
}

.btn_login {
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

.btn_login:hover {
  background-color: #86bfff;
  color: #f4fafd;
}
</style>