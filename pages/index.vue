<template>
  <div class="holder container">
    <!-- TODOS NOTIFICATION -->
    <h1 class="textCenter" v-if="todoCount > 0">"{{ todoCount }}" Todo(s) left</h1>
    <HomeBox />
  </div>
</template>

<script>
import HomeBox from "@/components/HomeBox"
export default {
  components: {
    HomeBox
  },
  data() {
    return {
      todoCount: 0
    }
  },
  mounted() {
    // Show todo nums (only unmarked)
    let todos = JSON.parse(localStorage.getItem("todoList"));
    if (todos) {
      todos.forEach(todo => {
        if (todo.checked !== true) {
          this.todoCount++;
        }
      });
    }
  }
}
</script>

<style scoped>
.holder {
  height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
}

.holder h1 {
  font-family: var(--sketch);
  margin-bottom: 6%;
  font-size: 42px;
}

/* MEDIA QUERIES */
@media screen and (max-width: 420px) {
  .holder {
    height: max-content;
    margin: 10% 0;
  }
}

@media screen and (max-width: 340px) {
  .holder h1 {
    font-size: 32px;
  }
}
</style>
