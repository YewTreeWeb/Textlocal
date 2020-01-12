<template>
  <div class="container">
    <header>
      <input type="text"
        name="new-todo"
        id="newTodo"
        placeholder="Add a new item."
        autofocus
        v-model="newTodo"
        @keyup.enter="addTodo">
    </header>
    <section v-show="todos.length" v-cloak>
      <ul class="todo-items">
        <li class="todo-items__item" v-for="(todo, index) in todos" :key="todo.id">
          <div class="todo-items__content">
            <input class="todo-complete" type="checkbox" name="todo-complete" v-model="todo.completed">
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
export default {
  name: 'TodoList',
  data() {
    return {
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      todos: [
        {
          id: 1, title: 'Task 1', completed: false, editing: false,
        },
        {
          id: 2, title: 'Task 2', completed: false, editing: false,
        },
      ],
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
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {
        return;
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
        editing: false,
      });

      this.newTodo = '';
      this.idForTodo++;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
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
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container{ max-width: 1200px; margin: 0 auto; }
#newTodo{
  width: 100%;
  height: 80px;
  padding: 15px;
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
  color: #42b983;
}
.todo-items{
  &__item{
    display: flex;
    align-items: center;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-between;
    font-size: 18px;
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
