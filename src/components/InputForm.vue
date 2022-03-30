<template>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <div class="input-block">
        <span class="input-block__label">{{params.label}}</span>
        <input class="input-block__input"
        :type="params.input === 'pass' ? 'password' : params.input === 'email' ? 'email' : 'text'"
        :autocomplete="params.input === 'pass' ? 'password' : params.input === 'email' ? 'email' : 'tel'"
        :name="params.input === 'pass' ? 'password' : params.input === 'email' ? 'email' : 'tel'"
        v-model="input_data"
        v-maska="params.input === 'phone' ? '+7 (###) ###-##-##' : null"
        @change="finishWriting" />
        <span v-bind:class="{block__error: error !== ''}">{{error}}</span>
    </div>
</template>

<script>

import useVuelidate from '@vuelidate/core'
import {email, required, minLength, helpers} from '@vuelidate/validators'
export default {
    props: {
        params: {
            type: Object,
            required: true
        }
    },
    setup () {
    return { v$: useVuelidate() }
  },
    validations () {
        return {
            email: {
              email: helpers.withMessage('Неверная запись электронной почты', email),
              required: helpers.withMessage('Поле не может быть пустым', required)
              },
            password: {
              required: helpers.withMessage('Поле не может быть пустым', required)
            },
            phone: {
                required: helpers.withMessage('Поле не может быть пустым', required),
                minLength: helpers.withMessage('Введите номер телефона', minLength(18))
            }
        }
    },
    data() {
    return {
      email: '',
      phone: '',
      password: '',
      error: ''
    }
    },
    methods: {
  		finishWriting() {
            if (this.params.input === 'email') {
                this.email = this.input_data
                this.v$.email.$touch()
                if (this.v$.email.$invalid) {
  				    this.error = this.v$.email.$errors[0].$message
                    this.$emit('login', "")
  		        } else {
                      this.error = ''
                      this.$emit('login', this.email)
                }
  		    }
            else if (this.params.input === 'pass') {
                this.password = this.input_data
                this.v$.password.$touch()
                if (this.v$.password.$invalid) {
  				    this.error = this.v$.password.$errors[0].$message
                    this.$emit('login', "")
  		        } else {
                      this.error = ''
                      this.$emit('login', this.password)
                }
  		    }
            else if (this.params.input === 'phone') {
                this.phone = this.input_data
                this.v$.phone.$touch()
                if (this.v$.phone.$invalid) {
  				    this.error = this.v$.phone.$errors[0].$message
                    this.$emit('login', "")
  		        } else {
                      this.error = ''
                      this.$emit('login', this.phone)
                }
  		    }
        }
  	}
}

</script>

<style scoped>

* {
    box-sizing: border-box;
}

.input-block {
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.input-block__label {
    color: #7eb4fc;
    font-family: 'Roboto', sans-serif;
    font-weight: 500;
    font-size: 14px;

    margin-top: 20px;
    margin-bottom: 10px;
}

.input-block__input {
    border-radius: 15px;
    border: none;
    min-height: 30px;
    background-color: #f4fafd;

    font-family: 'Roboto', sans-serif;
    font-weight: 400;
    font-size: 14px;
    color: #7eb4fc;

    padding: 0 10px;
}

.input-block__input:focus {
    outline: none;
    border: solid 2px #7eb4fc;
}

.block__error {
    color: #FF0021;

    margin-left: 10px;
    margin-top: 5px;
}
</style>