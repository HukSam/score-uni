<template>
  <form @submit.prevent>
    <h4>Регистрация</h4>
    <my-input
      v-model="user.name"
      type="text"
      placeholder="Логин:"
    ></my-input>
    <my-input
      v-model="user.password"
      type="text"
      placeholder="Пароль:"
    ></my-input>
    <my-input
      v-model="user.password"
      type="text"
      placeholder="Подтверждение пароля:"
    ></my-input>
    <my-button
      @click="createUser"
    >
      Зарегистрироваться
    </my-button>
  </form>
</template>

<script>
import MyInput from '@/components/UI/MyInput'
import MyButton from '@/components/UI/MyButton'
// import firebase from 'firebase/app'

export default {
  components: {
    MyInput,
    MyButton
  },
  name: 'registration-form',
  data () {
    return {
      user: {
        name: '',
        password: ''
      }
    }
  },
  methods: {
    createUser () {
      this.user.id = Date.now()
      this.$emit('create', this.user)
      this.user = {
        name: '',
        password: ''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  font-size: 30px;
}
</style>
