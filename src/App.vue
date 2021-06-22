<template>
  <div class="tarefas">
    <div class="container">
      <section>
        <form @submit.prevent="adicioneTodos">
          <h1 class="title">criar tarefas</h1>
          <input type="text" placeholder="descrição" v-model="form.text" />
          <button>Adicionar</button>
        </form>
      </section>
      <section>
        <h1>tarefas á concluir</h1>
        <ul>
          <li v-for="todo in doneTodos" :key="todo">
            <p>{{ todo.text }}</p>
            <a class="destroy" @click="finalize(todo.text)"></a>
          </li>
        </ul>
      </section>
    </div>
    <div class="container" style="margin-top: 175px">
      <section>
        <h1>tarefas já concluida</h1>
        <ul>
          <li v-for="todo in finalTodos" :key="todo.text">
            <p>{{ todo.text }}</p>
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

interface Todos {
  text: string
  done: boolean
}

export default defineComponent({
  data() {
    return {
      todos: [] as Todos[],
      form: {
        text: ''
      }
    }
  },
 
  methods: {
    finalize(text: Todos['text']) {
      console.log
      const index = this.todos.findIndex((todo) => todo.text === text)
      this.todos[index].done = true
    },
    adicioneTodos() {
      const novosTodos = { text: this.form.text, done: false }
      this.todos.push(novosTodos)
    }
  },
  computed: {
    doneTodos(): Todos[] {
      return this.todos.filter((todo) => !todo.done)
    },
    finalTodos(): Todos[] {
      return this.todos.filter((todo) => todo.done)
    }
  }
})
</script>
<style scoped>
.tarefas {
  display: flex;
}
button {
  background-color: #2d6cea;
  color: #e1e8ef;
  border: none;
  border-radius: 1rem;
  padding: 0.6rem 1.5rem;
  width: max-content;
  transition: all 0.3s linear;
  outline: none;
  cursor: pointer;
  box-shadow: 0 0 5px 3px rgba(45, 108, 234, 0.3);
  margin-top: 5px;
}

button:hover {
  background-color: #1b5cdc;
}
.container {
  margin: 4rem auto;
  max-width: 500px;
  width: 90%;
  display: grid;
  grid-gap: 2.5rem;
}

.title {
  font-size: 1rem;
  font-weight: 500;
  margin: 0.7rem 0;
}
input {
  width: 40em;
  background: transparent;
  border: 1px solid #999fc6;
  border-radius: 1rem;
  padding: 0.6rem;
  outline: none;
  color: #e1e8ef;
}
p {
  margin: 0;
}

ul {
  padding: 0;
  margin: 0;
  display: grid;
  grid-gap: 1rem;
}

li {
  background-color: #2b3a4e;
  padding: 1.2rem 1rem;
  border-radius: 1rem;
  position: relative;
  list-style: none;
  color: #8b98a8;
}
.destroy {
  background-color: #d53e6b;
  width: 24px;
  height: 24px;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.2s linear;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  right: 1.3rem;
}

.destroy:before,
.destroy:after {
  content: '';
  width: 3px;
  height: 13px;
  background-color: #ececf6;
  border-radius: 1rem;
  position: absolute;
  top: 50%;
  left: 50%;
}

.destroy:before {
  transform: translate(-50%, -50%) rotate(45deg);
}

.destroy:after {
  transform: translate(-50%, -50%) rotate(130deg);
}

.destroy:hover {
  background-color: #984848;
}
</style>
