<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" />
    <span class="addContainer" @click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        Error!

        <i
          class="closeModalBtn fa fa-times"
          aria-hidden="true"
          @click="showModal = false"
        >
        </i>
      </h3>
      <p slot="body">please input something.</p>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal';

export default {
  data: function() {
    return {
      newTodoItem: '',
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        const text = this.newTodoItem.trim();
        this.$store.commit('addOneItem', text);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    },
  },
  components: {
    Modal,
  },
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  border: 1px black #42b983;
  padding: 0.2rem;
  border-radius: 25%;
  margin-left: 20px;
  color: #42b983;
  cursor: pointer;
}
</style>
