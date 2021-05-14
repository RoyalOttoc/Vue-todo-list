<template>
  <div id="app">
    <TodoHeader />
    <TodoInput @addItem="addOneItem" />
    <TodoList
      :propsdata="todoItems"
      @removeItem="removeOneItem"
      @toggleItem="toggleOneItem"
    />
    <TodoFooter @clearAll="clearAllItems" />
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter';
import TodoHeader from './components/TodoHeader';
import TodoInput from './components/TodoInput';
import TodoList from './components/TodoList';

export default {
  data: function() {
    return {
      todoItems: [],
    };
  },
  methods: {
    addOneItem(todoItem) {
      const obj = { completed: false, item: todoItem };
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem(todoItem, index) {
      this.todoItems.splice(index, 1);
      localStorage.removeItem(todoItem.item);
    },
    toggleOneItem(todoItem) {
      todoItem.completed = !todoItem.completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems() {
      this.todoItems = [];
      localStorage.clear();
    },
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
  components: {
    TodoFooter,
    TodoHeader,
    TodoInput,
    TodoList,
  },
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f8;
  width: 50%;
  margin: auto;
}
@media screen and (max-width: 1024px) {
  body {
    width: 80%;
  }
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
