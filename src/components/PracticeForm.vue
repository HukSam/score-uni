<template>
  <form @submit.prevent>
    <h4>Создание практики</h4>
      <my-input
        v-model="practice.name"
        type="text"
        placeholder="Название практики"
      > </my-input>
      <my-input
        v-model="practice.points"
        type="text"
        placeholder="Баллы"
      ></my-input>
      <my-button
        @click="createPractice"
      >
        Добавить
      </my-button>
  </form>
</template>

<script>
import MyInput from '@/components/UI/MyInput'
import MyButton from '@/components/UI/MyButton'

export default {
  components: {
    MyInput,
    MyButton
  },
  name: 'practice-form',
  data () {
    return {
      practice: {
        name: '',
        points: ''
      }
    }
  },
  methods: {
    createPractice () {
      this.practice.id = Date.now()
      this.$emit('create', this.practice)
      this.practice = {
        name: '',
        points: ''
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

img {
  max-width: 25px;
  min-width: 25px;
}
</style>
