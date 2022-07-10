<template>
  <div v-if="groups.length > 0">
    <h3>Список групп</h3>
    <group-item
      v-for="group in groups"
      :group="group"
      :key="group.id"
      @remove="$emit('remove',group)"
    ></group-item>
  </div>
  <h2 style="color:red" v-else>
    Список команд пуст
  </h2>
</template>

<script>
import GroupItem from '@/components/GroupItem'
export default {
  components: {
    GroupItem
  },
  data () {
    return {
      studentPractice:
        [
        ]
    }
  },
  props: {
    groups: {
      type: Array,
      required: true
    }
  }

}
</script>

<style scoped>

</style>
