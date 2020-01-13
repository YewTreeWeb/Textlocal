<template>
  <div class="container">
    <header class="todo-header">
      <input type="text"
        name="new-todo"
        class="newTodo-input"
        id="newTodo"
        placeholder="Add a new item."
        autofocus
        v-model="newTodo"
        @keyup.enter="addTodo">
        <button class="newTodo-btn" type="button" @click="addTodo">Add item</button>
    </header>
    <section v-show="todos.length" v-cloak>
      <ul class="todo-items">
        <li class="todo-items__item" v-for="(todo, index) in todos" :key="todo.id">
          <div class="todo-items__content">
            <input class="todo-complete" type="checkbox" name="todo-complete" v-model="todo.completed" @click="completedTodo">
            <p class="todo-title" :class="{ 'todo-title--completed' : todo.completed }" v-if="!todo.editing" @dblclick="editTodo(todo)">{{ todo.title }}</p>
            <input class="todo-edit" type="text" name="todo-edit" v-else v-focus v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)">
          </div>
          <p class="todo-remove" @click="removeTodo(index)">&times;</p>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
// localStorage persistence

const key = 'todos';

export default {
  name: 'TodoList',
  data() {
    return {
      newTodo: '',
      beforeEditCache: '',
      idForTodo: 1,
      todos: [],
    };
  },
  directives: {
    focus: {
      // directive definition
      inserted(el) {
        el.focus();
      },
    },
  },
  mounted() {
    if (typeof localStorage !== 'undefined') {
      if (localStorage.getItem(key)) {
        try {
          this.todos = JSON.parse(localStorage.getItem(key));
        } catch (e) {
          localStorage.removeItem(key);
          if (window.console) {
            console.error(e);
          }
        }
      }
    }
  },
  methods: {
    addTodo() {
      let todoID = this.todos.length + 1;
      if (this.newTodo.trim().length === 0) {
        return;
      }
      this.todos.push({
        id: todoID++,
        title: this.newTodo,
        completed: false,
        editing: false,
      });

      this.newTodo = '';
      // this.idForTodo++;
      this.saveTodo();
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.saveTodo();
    },
    completedTodo(event, index) {
      if (event.target.checked) {
        try {
          const parsed = JSON.parse(localStorage.getItem(key));
          parsed.splice(index, 1);
          localStorage.setItem('todos', JSON.stringify(parsed));
        } catch (e) {
          if (window.console) {
            console.error(e);
          }
        }
      } else {
        this.saveTodo();
      }
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEdit(todo) {
      if (todo.title.trim() === '') {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.editing = false;
      todo.title = this.beforeEditCache;
    },
    saveTodo() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$primary: #42b983;
$black: #000;

.container{ max-width: 1200px; margin: 0 auto; }
.todo-header{
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-flow: row wrap;
  #newTodo{
    width: 80%;
    height: 80px;
    padding: 15px;
  }
  .newTodo-btn{
    width: fit-content;
    background-color: $primary;
    border-radius: 5px;
    padding: 46px 30px;
    font-size: 18px;
    text-transform: uppercase;
    margin-left: 2%;
    cursor: pointer;
    box-shadow: 0 0 0 0 $black;
    transition: box-shadow 0.3s ease-in-out, background-color 0.3s ease-in-out;
    &:hover{
      background-color: lighten($primary, 2.5%);
      box-shadow: 0 0 7px -3px $black;
    }
  }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: $primary;
}
.todo-items{
  &__item{
    display: flex;
    align-items: center;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    font-size: 23px;
    .todo-title{
      &--completed{
        text-decoration: line-through;
      }
    }
    .todo-remove{
      cursor: pointer;
      font-size: 20px;
      &:hover{
        color: red;
      }
    }
    .todo-complete{
      margin-right: 10%;
    }
  }
  &__content{
    display: flex;
    align-items: center;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: flex-start;
    min-width: 200px;
    width: fit-content;
  }
}
</style>
