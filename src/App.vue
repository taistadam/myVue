<template>
  <div id="app">
    <h3>{{ title }}</h3>
    <!-- calls a template -->
    <ul>
      <li v-for="(item) in todos" :key="(item.index)">   
        <list-item 
          :todo="item" 
          @textEdited="textEdited(index, arguments[0])"
          @buttonDeleted="getRidOfIt(index)"
        ></list-item>
      </li>
    </ul>
    <!--<input :value="newTodoText"></input>
    the colon tells it to look for a variable -->
    <input v-model="newTodoText"></input>
    <!-- v-model: two-way-binding between the input field value & newTodoText -->
    <button @click="addTodo">Add</button>
  </div>
</template>

<script>
import ListItem from './components/ListItem'
//import declares a variable which is not related to the file name.

export default {
  name: 'app',
  components: {
    ListItem,
    //is the same as ListItem: ListItem, it's an object shorthand notation
    // the property refers to the tag name, the variable to the import variable
  },
  data: function() {
    return { 
      // object that gets returned once vue calls the data function
      newTodoText: "blabla",
      title: "Todo list",
      todos: ['first', 'second', 'third'],
    }
  },
  methods: {
    addTodo: function() {
      this.todos.push(this.newTodoText)
    },
    //deleteTodo: function(item) {
    //  this.todos.splice(this.todos.indexOf(item), 1)
      // fancy function to delete a part of an array
    textEdited: function(index, newtext)  {
      this.$set(this.todos, index, newtext)
    },
    getRidOfIt: function(index) {
      this.$delete(this.todos, index)
    }
  }

//the parameters of an event of a child component and the 
// event handler function it calls in the parent component 
// are connected
}

</script>

<style>

</style>
