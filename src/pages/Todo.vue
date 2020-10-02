<template>
  <q-page class="flex column">
    <q-input bottom-line bottom-slots v-model="text" placeholder="Add todo" class="q-pa-lg">
      <template v-slot:append>
        <q-btn round dense flat icon="add" @click="add(text)"/>
      </template>
    </q-input>
    <q-list bordered separator>
      <q-item
        v-for="(todoItem, index) in todoList"
        clickable
        :key="todoItem.title"
        v-ripple
        @click="todoItem.done = !todoItem.done"
        :class="{ 'done bg-blue-1' : todoItem.done}">
        <div class="q-gutter-sm">
          <q-checkbox v-model="todoItem.done"  @click="todoItem.done = !todoItem.done"/>
        </div>
        <q-item-section>{{ todoItem.title }}</q-item-section>
        <q-btn
          flat
          round
          dense
          @click.stop="deleteTodo(index)"
          color="primary"
          icon="delete"
        v-if="todoItem.done"/>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      text: '',
      style: '',
      todoList: []
    }
  },
  methods: {
    add (title) {
      this.todoList.push({
        title: title,
        done: false
      }).then(
        this.text = '',
        this.$q.notify({
          message: 'Task added',
          color: 'primary'
        })
      )
    },
    deleteTodo (index) {
      this.todoList.splice(index, 1)
      this.$q.notify({
        message: 'Task deleted',
        color: 'primary'
      })
    }
  },
  created () {
    if (this.done === true) {
      this.style = 'text-decoration: line-through; color: grey;'
    }
  }
}
</script>

<style lang="scss">
  .done {
    .q-item__section {
      text-decoration: line-through;
      color: #bbb;
    }
  }
</style>
