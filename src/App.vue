<template>
  <div class="container">
    <h1>{{ title }}</h1>

    <form v-on:submit.prevent>
      <input type="text" v-bind:placeholder="plc" v-model.trim="inputValue">
      <button class="btn add" v-if="!edit" v-on:click="addTask">Add</button>
      <button class="btn edit-1" v-if="edit" @click="editTask" v-on:click="addTask">Edit</button>
    </form>
    <hr>
    <ul v-if="taskArray.length">
      <li v-for="(item, index) in taskArray">
        <p>
          {{ index + 1 }}.
          {{ item }}
        </p>

        <div class="btns">
          <button class="btn del" v-on:click="deleteTask(index)">Delete</button>
          <button class="btn edit" @click="todo(index)">Edit</button>
        </div>
      </li>
    </ul>
    <h3 v-else>There are not tasks!</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'to do list',
      plc: 'Write a task',
      inputValue: '',
      taskArray: [
        'Make a cup of coffee',
        'Do a homework'
      ],
      edit: false,
      taskIndex: ''
    }
  },
  methods: {
    addTask() {
      if (this.inputValue) {
        this.taskArray.unshift(this.inputValue)
      }
      this.inputValue = ''
    },
    deleteTask(taskIndex) {
      this.taskArray.splice(taskIndex, 1)
    },
    todo(index) {
      this.inputValue = this.taskArray[index]
      this.edit = true
      this.taskIndex = index
    },
    editTask() {
      this.taskArray[this.taskIndex] = this.inputValue
      this.edit = false
      this.inputValue = ''
    }
  },
}
</script>

<style>
@import url(./assets/main.css);
</style>