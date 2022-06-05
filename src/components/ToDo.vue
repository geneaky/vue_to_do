<template>
  <div v-for="todo in todos" v-bind:key = "todo.text">
    <label>
      <input type="checkbox" v-model="todo.done">
      <span v-bind:class="{donestyle:todo.done}">{{ todo.text }}</span>
    </label>
  </div>
  <input type="text" v-model="addtext" v-on:keyup.enter="addToDo" placeholder="할 일"/>
  <p><button v-on:click="cleanToDo">처리완료 - 삭제</button></p>
  <p>{{remaining}} / {{todos.length}}건 처리</p>
</template>

<script>
export default {
  name: "ToDo",
  data: () => {
    return {
      addtext: '',
      todos: [
        {done:false, text: "운동하기"},
        {done:false, text: "Vue.js 공부하기"}
      ],

    }
  },
  computed: {
    remaining() {
      return this.todos.filter((todo)=> todo.done).length;
    }
  },
  methods: {
    addToDo() {
      this.todos = [...this.todos, {done:false, text:this.addtext}]
      this.addtext = '';
    },
    cleanToDo() {
      this.todos = this.todos.filter((todo) => !todo.done)
    }
  }
}
</script>

<style scoped>
  .donestyle {
    text-decoration: line-through;
    color: lightgray;
  }
</style>