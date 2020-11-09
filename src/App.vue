<template>
  <div id="app">
    <div v-if="isLoginOpen === true || isSignupOpen === true">
      <div>
        <LoginForm
          v-show="isLoginOpen"
          :userInput="userInput"
          :login="login"
          @handle-signup-click="
            isSignupOpen = !isSignupOpen;
            isLoginOpen = false;
            errors = [];
            messages = [];
          "
        />
        <SignupForm
          v-show="isSignupOpen"
          :userSignup="userSignup"
          :signup="signup"
          @handle-login-click="
            isLoginOpen = !isLoginOpen;
            isSignupOpen = false;
            errors = [];
            messages = [];
          "
        />
      </div>
      <div v-show="errors.length > 0">
        <h4 class="error" v-for="error in errors" :key="error">
          {{ error }}
        </h4>
      </div>
      <div v-show="messages.length > 0">
        <h4 class="message" v-for="message in messages" :key="message">
          {{ message }}
        </h4>
      </div>
    </div>

    <!-- todos -->
    <div v-if="isLoginOpen === false && isSignupOpen === false">
      <InputTodo
        :todoInput="todoInput"
        :userLogin="userLogin"
        :addNewTodo="addNewTodo"
      />
      <Todos :todos="todos" :deleteOne="deleteTodo" :setDone="disableTodo" />
    </div>
  </div>
</template>

<script>
import LoginForm from "./components/LoginForm";
import SignupForm from "./components/SignupForm";
import InputTodo from "./components/InputTodo";
import Todos from "./components/Todos";

export default {
  name: "App",
  components: {
    LoginForm,
    SignupForm,
    InputTodo,
    Todos,
  },
  data() {
    return {
      isLoginOpen: true,
      isSignupOpen: false,
      userInput: {
        name: "",
      },
      userLogin: {},
      userSignup: {
        name: "",
      },
      errors: [],
      messages: [],
      todoInput: {
        title: "",
      },
      todos: [],
    };
  },
  watch: {
    userLogin: function () {
      if (this.userLogin) {
        console.log("show todos");
        setTimeout(() => {
          this.isLoginOpen = false;
          this.isSignupOpen = false;
        }, 1000);
      }
    },
  },
  methods: {
    login: function () {
      let users = JSON.parse(localStorage.getItem("users"));
      if (!users) {
        users = [];
      }
      this.errors = [];
      this.messages = [];

      let getUser = users.find((user) => {
        return user.name === this.userInput.name;
      });
      setTimeout(() => {
        if (getUser) {
          this.messages.push("Loggin success!, welcomeback " + getUser.name);
          this.userLogin = getUser;
          let todos = JSON.parse(localStorage.getItem("todos"));
          if (!todos) {
            todos = [];
          }
          this.todos = todos.filter(
            (todo) => todo.userId === this.userLogin.id
          );
        } else {
          this.errors.push("Wrong username!");
        }
      }, 1000);
    },
    signup: function () {
      let users = JSON.parse(localStorage.getItem("users"));
      if (!users) {
        users = [];
      }
      this.errors = [];
      this.messages = [];
      users.forEach((user) => {
        if (user.name === this.userSignup.name) {
          this.errors.push("This name has already taken !");
          console.log("same name!");
        }
      });
      if (this.errors.indexOf("This name has already taken !") === -1) {
        users.push({
          id: Math.trunc(Math.random() * 1000000),
          name: this.userSignup.name,
        });
        localStorage.setItem("users", JSON.stringify(users));
        this.messages.push("Create account success, ready for login!");
      }
    },
    addNewTodo: function () {
      let todos = JSON.parse(localStorage.getItem("todos"));
      if (!todos) {
        todos = [];
      }
      let todoId= Math.trunc(Math.random() * 1000000);
      this.todos.push({
        id: todoId,
        userId: this.userLogin.id,
        title: this.todoInput.title,
        status: true,
      });
      todos.push({
        id: todoId,
        userId: this.userLogin.id,
        title: this.todoInput.title,
        status: true,
      });
      localStorage.setItem("todos", JSON.stringify(todos));
      this.todoInput.title = "";
    },
    deleteTodo: function (todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);

      let todos = JSON.parse(localStorage.getItem("todos"));
      if (!todos) {
        todos = [];
      }
      console.log("delete todo id: " + todoId);
      todos = todos.filter((todo) => todo.id !== todoId);
      localStorage.setItem("todos", JSON.stringify(todos));
    },
    disableTodo: function (todoId) {
      this.todos = this.todos.map((todo) => {
        if (todo.id === todoId) todo.status = !todo.status;
        return todo;
      });

      // let todos = JSON.parse(localStorage.getItem("todos"));
      // if (!todos) {
      //   todos = [];
      // }
      // todos = todos.filter((todo) => todo.id !== todoId);
      // localStorage.setItem("todos", JSON.stringify(todos));
    },
  },
};
</script>

<style>
#app {
  font-family: Helvetica, sans-serif;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-top: 5rem;
}

h1,
h2,
h3,
h4,
h5 {
  font-weight: 200;
  margin: 1rem 0;
}
.error {
  color: rgb(255, 50, 50);
}
.message {
  color: #4bb543;
}
</style>
