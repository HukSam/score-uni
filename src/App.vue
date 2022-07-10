<template>
  <div class="app">
    <div class="wrapper">
      <div class="nav-menu">
        <div class="item group"><h2>ГРУППА: О-20-ПРИ</h2></div>
        <div class="item mode"><h2>РЕЖИМ:</h2></div>
        <div class="item auth">
          <my-button
            @click="showUserAuth"
          >
            ВХОД / РЕГИСТРАЦИЯ
          </my-button>
          <my-dialog v-model:show="authVisible">
            <registration-form
              @create="createUser"
            />
          </my-dialog>
        </div>
      </div>
      <div class="mainBody">
        <div class="item teacher"><h2>Преподаватель: Коптенок Е.В.</h2></div>
        <div class="item groups">
          <div class="block-add-group">
            <h1>Страница с группами</h1>
            <my-button
              @click="showDialog"
            >
              Создать команду
            </my-button>
                <my-dialog v-model:show="dialogVisible">
              <group-form
                @create="createGroup"
              />
            </my-dialog>

            <div class="wrapper-groups">
              <group-list
                :groups="groups"
                @remove="removeGroup"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import GroupForm from '@/components/GroupForm'
import GroupList from '@/components/GroupList'
import MyButton from '@/components/UI/MyButton'
import MyDialog from '@/components/UI/MyDialog'
import RegistrationForm from '@/components/RegistrationForm'
import { doc, setDoc, updateDoc, deleteField, arrayUnion } from 'firebase/firestore'
import { db } from '@/main'

export default {
  components: {
    MyButton,
    GroupForm,
    GroupList,
    MyDialog,
    RegistrationForm
  },
  data () {
    return {
      groups: [

      ],
      dialogVisible: false,
      authVisible: false,
      groupIndex: 0,
      studentIndex: 0
    }
  },
  methods: {
    async createGroup (group) {
      this.groups.push(group)
      const userRef = doc(db, 'groups', 'OCMGQFjLs6b3K5FCEqeV5FIJrmH2')
      await setDoc(userRef, {
        group
      })
      await updateDoc(userRef, {
        group: arrayUnion()
      })
      this.dialogVisible = false
    },
    async removeGroup (group) {
      this.groups = this.groups.filter(g => g.id !== group.id)
      const userDel = doc(db, 'groups', 'OCMGQFjLs6b3K5FCEqeV5FIJrmH2')
      await updateDoc(userDel, {
        group: deleteField()
      })
    },

    showDialog () {
      this.dialogVisible = true
    },
    showUserAuth () {
      this.authVisible = true
    }
  }
}
</script>

<style>
button {
  padding: 0;
}

html, body {
  margin: 0;
  padding: 0;
  height: 100vh;
  line-height: 1;
  font-size: 14px;
  background-color: whitesmoke;
  font-family: Arial, sans-serif;
}

.wrapper {
  height: 100vh;
  display: grid;
  grid-template-rows: 1fr 7fr;
}

.wrapper h2 {
  font-size: 24px;
  text-align: center;
  vertical-align: center;

}

.wrapper .mode h2 {
  color: red;
}

.nav-menu {
  padding: 10px;
  display: grid;
  grid-template-columns: repeat(3,1fr);
  grid-gap: 10%;
  border-bottom: 3px solid black;
}

.mainBody {
  display: grid;
  grid-template-rows: 1fr 6fr;
}

.mainBody .teacher{
  border-bottom: 3px solid black;
}

.mainBody .groups {
  display: grid;
  grid-template-columns: 1fr 1fr;

}

.mainBody .groups .item {
  display: grid;
  grid-template-columns: 4fr 2fr 1fr 1fr 1fr;
  border: 2px solid red;
}

.mainBody .groups .item *{
  max-height: 35px;
  border: 2px solid red;
}
</style>
