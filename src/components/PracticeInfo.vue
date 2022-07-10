<template>
  <div class="wrapper-practice-info-add">
    <h2>Информация о практиках</h2>
    <my-button
      @click="showDialog"
    >
      Добавить практику
    </my-button>
    <my-dialog v-model:show="dialogVisible">
      <practice-form
        @create="createPractice"
      />
    </my-dialog>
      <practice-list
        :practices="practices"
      >
      </practice-list>
  </div>
</template>

<script>
import PracticeForm from '@/components/PracticeForm'
import PracticeList from '@/components/PracticeList'
import MyDialog from '@/components/UI/MyDialog'
import MyButton from '@/components/UI/MyButton'
import { deleteField, doc, setDoc, updateDoc } from 'firebase/firestore'
import { db } from '@/main'

export default {
  component: {
    PracticeForm,
    PracticeList,
    MyDialog,
    MyButton
  },
  data () {
    return {
      practices:
        [
        ],
      dialogVisible: false
    }
  },
  props: {
    student: {
      type: Object,
      required: true
    }
  },
  name: 'practice-info',
  methods: {
    async createPractice (practice) {
      this.practices.push(practice)
      const userRef = doc(db, 'practice', 'BwRAab6s5Z1J7b73ovgA')
      await setDoc(userRef, {
        practice
      })
      this.dialogVisible = false
    },
    async removePractice (practice) {
      this.practices = this.practices.filter(g => g.id !== practice.id)
      const userDel = doc(db, 'student', 'BwRAab6s5Z1J7b73ovgA')
      await updateDoc(userDel, {
        practice: deleteField()
      })
    },
    showDialog () {
      this.dialogVisible = true
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

.wrapper-practice-info-add {
  display: grid;
}

</style>
