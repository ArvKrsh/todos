<template>
  <div class="container">
    <p>{{ title }}</p>
    <div class="input-container">
      <input
        type="text"
        name="new-todo"
        id="new-todo"
        placeholder="What do you want to do ?"
      />
      <button @click="addNewTodo($event)">Add</button>
    </div>
    <div id="todos-list">
      <div v-for="todo in todos" :key="todo.id" class="todo-single">
        <input
          class="box"
          type="checkbox"
          name="todo"
          :id="todo.id"
          :value="todo.id"
          @click="toggleCheckbox($event)"
          :checked="todo.completed"
        />
        <label :for="todo"> {{ todo.todo_name }}</label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      title: "Todos",
      todos: []
    };
  },
  methods: {
    toggleCheckbox(event) {
      console.log(event.currentTarget.id);
      const id  = event.currentTarget.id;
      this.todos = this.todos.map(todo => 
        todo.id == id ? {...todo, completed: !todo.completed} : todo
        )
      console.log(this.todos)
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    addNewTodo() {
      let todo = { 
        id : Math.floor(Date.now() * Math.random()),
        todo_name : document.getElementById('new-todo').value,
        completed : false
       }
      this.todos.push(todo);
      localStorage.setItem('todos', JSON.stringify(this.todos))
      /*chrome.storage.sync.set(
        {"todos": this.todos},
        function () {
          alert('saved')
        }
      );*/
      document.getElementById('new-todo').value = ""
    },
  },
  mounted(){
      let todos = localStorage.getItem('todos');
      console.log(todos)
      if(todos) {
        let jsonObj = JSON.parse(todos)
        this.todos = jsonObj;
      }
      /*chrome.storage.sync.get(
        "todos",
        function (todos) {
          this.todos = todos;
        }
      );*/
  }
};
</script>

<style scoped>
p {
  margin-top: 15px;
  font-size: 20px;
  text-align: center;
  letter-spacing: 2px;
  margin-bottom: 5px;
}
#new-todo {
  width: 70%;
  margin: 20px 0px;
}
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin: 20px 0px
}
.input-container {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.todo-single {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin: 5px 30px;
}
#todos-list {
  width: 100%;
  display: flex;
  flex-direction: column;
}
label {
  margin-left: 15px;
}
input[type='text'] {
  padding: 5px;
}
button {
  padding: 5px 15px;
  background-color: rgb(53, 53, 240);
  color: white;
  border-color: rgb(53, 53, 240);
  border-radius: 3px;
}
::placeholder { /* Most modern browsers support this now. */
   color:rgb(177, 177, 177);
}
.box {
  margin: 3px 0px;
}
</style>
