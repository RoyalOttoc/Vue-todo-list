<template>
  <div id="app">
    <TodoHeader />
    <TodoInput />
    <TodoList />
    <TodoFooter />
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter';
import TodoHeader from './components/TodoHeader';
import TodoInput from './components/TodoInput';
import TodoList from './components/TodoList';

export default {
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
