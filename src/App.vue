<template>
  <div class="container">
    <h1>{{ title }}</h1>

    <form @submit.prevent>
      <textarea type="text" :placeholder="plc" v-model.trim="inputValue"></textarea>
      <button v-if="!isEditing" class="btn add" @click="addTask">Add</button>
      <button v-else class="btn edit" @click="saveTask(index)">Save</button>
    </form>
    <hr>
    <ul v-if="taskArray.length">
      <li v-for="(item, index) in taskArray" :key="item">
        <p :class="{ long: item.length > 155 }">
          {{ index + 1 }}.
          {{ item }}
        </p>

        <div class="btns">
          <button v-if="!isEditing" class="btn del" @click="deleteTask(index)">Delete</button>
          <button class="btn edit" @click="editTask(item, index)">Edit</button>
          <!-- v-if="!clickedIndex != index" -->
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
      taskArray: [],
      isEditing: false,
      clickedIndex: null,
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
      const answer = confirm('Are you sure to delete?')
      if (answer) {
        this.taskArray.splice(taskIndex, 1)
      } else {
        alert('You cancelled action!')
      }
    },
    editTask(taskValue, taskIndex) {
      this.isEditing = true
      this.inputValue = taskValue
      this.clickedIndex = taskIndex
    },
    saveTask() {
      this.taskArray[this.clickedIndex] = this.inputValue
      this.isEditing = !this.isEditing
      this.inputValue = ''
    }
  },
}
</script>

<style>
@import url(./assets/main.css);
</style>