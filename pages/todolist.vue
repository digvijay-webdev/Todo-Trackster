<template>
  <div>
    <!-- HEADER COMPONENT -->
    <Header title="Todo List" />

    <!-- RENDERING TODO-LIST -->
    <div class="container">
      <div class="listWrapper">
        <div class="todoItem" v-for="todo in todoList" :key="todo.id">
          <h2 ref="todoTitles">{{ todo.task }}</h2>
          <div class="todoControls">
            <span @click="deleteTodo" class="cross">&times;</span>
            <span @click="markTodo" class="check">&check;</span>
          </div>
          <div class="date">
            {{ todo.dateCreated }}
          </div>
        </div>
      </div>
    </div>

    <!-- FIXED INPUT FIELD -->
    <div ref="toggler" class="todoInput">
      <div class="container">
        <form @submit.prevent="addTodo">
          <input v-model="todoInput" name="todoTxt" placeholder="todo here.." minlength="6" maxlength="40" required>
          <button type="submit">Add Todo</button>
        </form>
      </div>
    </div>

    <!-- TODO-INPUT TOGGLE BUTTON -->
    <div @click="toggleInputField" ref="toggleCloseOnSubmit" class="toggler">
      &times;
    </div>
  </div>
</template>

<script>
import Header from "~/components/Header"
export default {
  components: {
    Header
  },
  data() {
    return {
      todoInput: '',
      todoList: null
    }
  },
  methods: {
    addTodo() {
      // Creating Todo Class
      class Todo {
        constructor(id, task, checked, dateCreated) {
          this.id = id,
          this.task = task,
          this.checked = checked,
          this.dateCreated = dateCreated
        }
      }

      // Getting date
      let date = new Date();
      let month = date.getMonth();
      let day = date.getDate();
      let year = date.getFullYear();
      let FullDate = `${day}/${month + 1}/${year}`;

      // Random number for id
      const r_id = Math.ceil(Math.random() * 2000) + 1;

      // Creating Todo Instance
      let todoObj = new Todo(r_id, this.todoInput, false, FullDate);
      
      // Storing in LS
      let data = localStorage.getItem("todoList");
      if (data == null || data == undefined) {
        let todoArr = [];
        todoArr.push(todoObj);
        localStorage.setItem("todoList", JSON.stringify(todoArr));

        // Getting list from LS and rendering
        this.todoList = JSON.parse(localStorage.getItem("todoList"));
      } else {
        let todoList = JSON.parse(data);
        todoList.push(todoObj);
        localStorage.setItem("todoList", JSON.stringify(todoList));

        // Getting list from LS and rendering
        this.todoList = JSON.parse(localStorage.getItem("todoList"));
      }
      this.todoInput = "";
      this.$refs.toggler.classList.remove("opened");
      this.$refs.toggleCloseOnSubmit.style.transform = "rotateZ(44deg)";
    },

    // delete todos
    deleteTodo(e) {
      let todoList_LS = JSON.parse(localStorage.getItem("todoList"));
      todoList_LS.forEach(todo => {
        if (todo.task == e.path[2].firstChild.textContent) {
          todoList_LS.splice(todoList_LS.indexOf(todo), 1); // finding and removing an item
          localStorage.setItem("todoList", JSON.stringify(todoList_LS));

          // refresh the todoList property in data object
          this.todoList = JSON.parse(localStorage.getItem("todoList"));
        }
      });
    },

    // mark todos
    markTodo(e) {
      let todoList_LS = JSON.parse(localStorage.getItem("todoList"));
      todoList_LS.forEach(todo => {
        if (todo.task == e.path[2].firstChild.textContent) {
          if (todo.checked == false) {
            todo.checked = true;
            localStorage.setItem("todoList", JSON.stringify(todoList_LS));

            e.path[2].firstChild.style.textDecoration = "line-through";
          } else {
            todo.checked = false;
            localStorage.setItem("todoList", JSON.stringify(todoList_LS));

            e.path[2].firstChild.style.textDecoration = "";
          }
      }});
    },

    // toggle Input Field
    toggleInputField(e) {
      this.$refs.toggler.classList.toggle("opened");
      
      if (this.$refs.toggler.classList[1] == "opened") {
        e.path[0].style.transform = "rotateZ(0deg)";
      } else {
        e.path[0].style.transform = "rotateZ(44deg)";
      }
    },

    // quick fix for checkMark bug
    refreshTodoListOnMounted() {
      this.todoList = JSON.parse(localStorage.getItem("todoList"));
      setTimeout(() => {
        let todoTitles = this.$refs.todoTitles;
        for (let i = 0; i < this.todoList.length; i++) {
          if (this.todoList[i].task == todoTitles[i].textContent && this.todoList[i].checked == true) {
            todoTitles[i].style.textDecoration = "line-through";
          }
        }
      }, 300);
    }
  },
  mounted() {
    this.refreshTodoListOnMounted();
  }
}
</script>

<style scoped>
/* TODO INPUT SECTION */
.todoInput {
  background-color: var(--white);
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  position: absolute;
  top: 0;
  right: 0;
  transform: translateX(-100%);
  transition: all 0.3s ease;
}

.opened {
  transform: translateX(0);
}


.todoInput form {
  width: 50%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}

.todoInput form input {
  font-size: 20px;
  text-align: center;
  color: #414141;
  padding: 6px 0;
  outline: none;
  border: 1px solid #777;
  border-radius: 4px;
  margin-bottom: 2px;
}

.todoInput form button {
  font-size: 20px;
  color: var(--white);
  background-color: var(--dark);
  padding: 4px 0;
  cursor: pointer;
  border: none;
  border-radius: 4px;
  outline: none;
  cursor: pointer;
}

.todoInput form button:hover {
  background-color: #3b4250;
}


/* TODO INPUT TOGGLE BUTTON */
.toggler {
  width: 60px;
  height: 60px;
  position: absolute;
  bottom: 0;
  right: 0;
  margin: 0 12px 12px 0;
  background-color: #f7f7f7;
  border-radius: 100%;
  color: var(--dark);
  font-size: 42px;
  font-weight: 600;
  text-align: center;
  transform: rotateZ(44deg);
  cursor: pointer;
  transition: all 0.3s ease;
}



/* TODO LIST SECTION */
.listWrapper {
  margin-top: 18px;
}

.listWrapper .todoItem {
  position: relative;
  background-color: var(--white);
  margin-bottom: 2px;
  padding: 4px 8px;
  border-radius: 4px;
  box-shadow: 0 2px 2px #888;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.listWrapper .todoItem h2 {
  color: var(--dark);
  font-family: var(--magic);
  padding-bottom: 10px;
}

.listWrapper .todoItem span {
  padding: 0 8px;
  font-size: 24px;
  cursor: pointer;
  border-radius: 4px;
}
.listWrapper .todoItem span:hover {
  background-color: #cfcfcf;
}

.listWrapper .todoItem .todoControls {
  width: max-content;
  display: flex;
  flex-direction: row;
}

.listWrapper .todoItem .todoControls .cross {
  color: var(--red);
}

.listWrapper .todoItem .todoControls .check {
  color: var(--green);
}

.listWrapper .todoItem .date {
  color: #333;
  font-size: 10px;
  position: absolute;
  bottom: 0;
  left: 0;
  margin: 4px 8px 0 8px;
}

/* MEDIA QUERIES */
@media screen and (max-width: 840px) {
  .listWrapper .todoItem h2 {
    font-size: 18px;
  }
  .todoInput form {
    width: 90%;
  }
}

@media screen and (max-width: 620px) {
  .listWrapper .todoItem h2 {
    font-size: 16px;
  }
}
</style>
