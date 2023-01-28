<template>
  <div class="todo__container">
    <input
      type="text"
      class="todo__input"
      placeholder="Que devez-vous faire ?"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <div class="todo__footer">
      <button @click="filterTodo('All')">Tous</button>
      <button @click="filterTodo('Not-completed')">A faire</button>
      <button @click="filterTodo('Completed')">Faite</button>
    </div>
    <ul class="todo__list" v-if="todos.length > 0">
      <transition-group name="fade" appear>
        <li class="todo__item" :key="todo.id" v-for="todo in filteredTodo">
          <input
            type="checkbox"
            class="todo__checkbox"
            :id="todo.id"
            v-model="todo.completed"
          />
          <label
            class="todo__label"
            @dblclick="editTodo(todo.id)"
            :class="{ checked: todo.completed }"
            v-show="editingTodo !== todo.id"
            v-if="addTodo"
          >
            {{ todo.title }}
          </label>
          <input
            v-model="todo.title"
            class="todo__edit_input"
            type="text"
            v-if="editingTodo === todo.id"
            @keyup.enter="doneEdit"
            @keyup.esc="cancelEdit"
            v-focus="editingTodo === todo.id"
            @blur="doneEdit"
          />
          <button
            class="todo__button_delete"
            type="button"
            @click.prevent="deleteTodo(todo.id)"
          >
            <icon-cross width="20" height="20" />
          </button>
        </li>
      </transition-group>
    </ul>
    <span v-if="filteredTodo.length === 0">Vous n'avez aucune tâche à faire</span>
  </div>
</template>

<script>
import Vue from "vue";
import IconCross from "./icons/IconCross.vue";
const randomId = () => Math.floor(Math.random() * 1000);
export default {
  components: {
    IconCross,
  },
  directives: {
    focus(el, value) {
      if (value) {
        Vue.nextTick(() => el.focus());
      }
    },
  },
  name: "todo-list",
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Apprendre SailsJS",
          completed: false,
        },
        {
          id: 2,
          title: "Apprendre VueJS",
          completed: false,
        },
        {
          id: 3,
          title: "Créer une stack complète avec SailsJS et VueJS",
          completed: false,
        },
      ],
      filteredTodo: [],
      newTodo: "",
      editingTodo: null,
      oldTitleTodo: "",
    };
  },
  methods: {
    addTodo() {
      if (!this.newTodo || this.newTodo.trim().length === 0) return;
      this.todos.push({
        id: randomId(),
        title: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
    },
    editTodo(todoId) {
      this.editingTodo = todoId;
      this.oldTitleTodo = this.todos.find((t) => t.id === todoId).title;
    },
    doneEdit() {
      this.editingTodo = null;
    },
    cancelEdit() {
      this.todos.find((t) => t.id === this.editingTodo).title = this.oldTitleTodo;
      this.editingTodo = null;
    },
    filterTodo(filter) {
      if (filter === "All") {
        this.filteredTodo = this.todos;
      } else if (filter === "Not-completed") {
        this.filteredTodo = this.todos.filter((todo) => todo.completed === false);
      } else if (filter === "Completed") {
        this.filteredTodo = this.todos.filter((todo) => todo.completed === true);
      }
    },
  },
};
</script>

<style src="../styles/todo.scss" lang="scss"></style>
