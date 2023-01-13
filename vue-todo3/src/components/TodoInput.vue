<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>

    <!-- use the modal component, pass in the prop -->
    <TodoModal :show="showModal" @close="showModal = false">
      <template #header>
        <h3>
          경고!
          <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
        </h3>
      </template>
      <template #body>
        <div>할일을 입력해 주세요.</div>
      </template>
    </TodoModal>
  </div>
</template>

<script>
import TodoModal from "@/components/common/TodoModal";

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        // this.$emit('addTodoItem', this.newTodoItem);
        const text = this.newTodoItem.trim();
        this.$store.commit('addOneItem', text);
        this.clearInput();
      } else {
        this.showModal = true;
      }
    },
    // 인풋 지우기
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components: {
    TodoModal,
  }
}
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
  font-size: 0.9em;
}

.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

.addBtn {
  color: white;
  vertical-align: middle;
}

.closeModalBtn {
  color: #42b983;
}
</style>