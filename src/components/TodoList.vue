<template>
  <div id="app">
    <h1>Coisas a fazer?</h1>
    <form @submit.prevent="createTodo()">
      <input type="text" placeholder="Todo" v-model="form.text" />

      <label class="checkbox-input">
        {{ form.done ? 'Concluída' : 'Não concluída' }}
        <input type="checkbox" v-model="form.done" :checked="form.done" />
        <span class="checkmark"></span>
      </label>

      <button type="submit">Adicionar</button>
    </form>

    <ul class="todos">
      <span class="todos-title">Todos</span>
      <li
        v-for="todo in todos"
        :key="todo.id"
        :class="['todo', { done: todo.done }]"
      >
        <label class="checkbox-input" @click="toogleTodoStatus(todo)">
          <input type="checkbox" :checked="todo.done" />
          <span class="checkmark"></span>
        </label>
        <span class="todo-text">{{ todo.text }}</span>
        <a class="todo-delete" @click="destroy(todo)"></a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      todos: [],
      form: {
        id: 0,
        text: '',
        done: false
      }
    }
  },
  methods: {
    createTodo() {
      const data = {
        id: this.form.id + 1,
        text: this.form.text,
        done: this.form.done
      }
      this.todos.push(data)

      this.form = {
        id: data.id,
        text: '',
        done: false
      }
    },
    toogleTodoStatus(todo) {
      const data = {
        ...todo,
        done: todo.done === true ? false : true
      }

      const index = this.todos.findIndex(({ id }) => id === data.id)
      this.todos[index] = data
    },
    destroy(todo) {
      const data = { ...todo }

      const index = this.todos.findIndex(({ id }) => id === data.id)
      this.todos.splice(index, 1)
    }
  }
}
</script>

<style scoped>
h1 {
  color: #8b98a8;
  font-size: 36px;
}

form {
  display: grid;
  grid-gap: 1.5rem;
}
form input {
  background-color: transparent;
  border: 1px solid #999fc6;
  border-radius: 0.9rem;
  padding: 0.7rem;
  width: 100%;
  font-size: 16px;
  outline: none;
  color: #ececf6;
  box-sizing: border-box;
}

form input::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

form button[type='submit'] {
  background-color: #2d6cea;
  padding: 0.5rem 1rem;
  color: #ececf6;
  border-radius: 0.5rem;
  border: none;
  outline: none;
  width: max-content;
  padding: 0.7rem 1.5rem;
  padding-right: 2.5rem;
  position: relative;
  font-size: 1rem;
  border-radius: 0.9rem;
  cursor: pointer;
  box-shadow: 0px 0 13px 2px rgba(45, 108, 234, 0.3);
  transition: all 0.2s linear;
}

form button[type='submit']:hover {
  background-color: #1b5cdc;
}

form .checkbox-input {
  margin-left: 0.5rem;
}

form button[type='submit']:after {
  content: '+';
  position: absolute;
  right: 1.2rem;
  font-size: 20px;
  font-weight: 100;
  top: 50%;
  transform: translateY(-50%);
}

.todos {
  padding: 0;
  display: grid;
  grid-gap: 0.5rem;
}

.todos-title {
  color: #ececf6;
}

.todo {
  color: #ececf6;
  background-color: #2b3a4e;
  padding: 1rem;
  border-radius: 0.9rem;
  display: grid;
  grid-template-columns: max-content 1fr auto;
  justify-content: start;
  grid-gap: 0.3rem;
}

.todo .todo-text {
  width: max-content;
  color: #8b98a8;
  align-self: center;
}

.todo .todo-delete {
  background-color: #d53e6b;
  width: 24px;
  height: 24px;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.2s linear;
  position: relative;
}

.todo .todo-delete:before,
.todo .todo-delete:after {
  content: '';
  width: 3px;
  height: 13px;
  background-color: #ececf6;
  position: absolute;
  top: 50%;
  left: 50%;
}

.todo .todo-delete:before {
  transform: translate(-50%, -50%) rotate(45deg);
}

.todo .todo-delete:after {
  transform: translate(-50%, -50%) rotate(130deg);
}

.todo .todo-delete:hover {
  background-color: #984848;
}

.todo.done .todo-text {
  text-decoration: line-through;
}

/* checkbox */
.checkbox-input {
  display: block;
  position: relative;
  padding-left: 35px;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  width: max-content;
  color: #ececf6;
}

.checkbox-input input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: transparent;
  border: 1px solid #ececf6;
  border-radius: 0.4rem;
}

.checkbox-input input:checked ~ .checkmark {
  background-color: #2d6cea;
  border: 1px solid #2d6cea;
}

.checkmark:after {
  content: '';
  position: absolute;
  display: none;
}

.checkbox-input input:checked ~ .checkmark:after {
  display: block;
}

.checkbox-input .checkmark:after {
  left: 7px;
  top: 3px;
  width: 4px;
  height: 8px;
  border: solid #ececf6;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
