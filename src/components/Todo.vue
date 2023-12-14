<template>
  <div class="max-w-xl space-y-5 py-10 mx-auto">
    <h2 class="text-5xl text-center text-red-400">Todo List</h2>
    <div class="flex items-center gap-x-2">
      <input
        class="w-full bg-transparent flex outline-none border border-white px-2 text-white rounded items-center h-9"
        v-model="newTodo"
        placeholder="Add a new todo"
      />
      <button
        @click="addTodo"
        class="h-9 px-4 rounded hover:bg-pink-600 inline-flex items-center bg-green-500 text-white font-medium"
      >
        ADD
      </button>
    </div>
    <ul class="space-y-4">
      <li
        class="bg-blue-400 text-white flex items-center justify-between px-3 py-2 rounded text-xl"
        v-for="(todo, index) in todos"
        :key="index"
      >
        <div
          v-if="editIndex !== index"
          class="flex items-center flex-1 justify-between"
        >
          <span> {{ todo }}</span>
          <div class="flex items-center gap-x-2">
            <button @click="editTodo(index)">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6 text-slate-50"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10"
                />
              </svg>
            </button>
            <button @click="removeTodo(index)">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6 text-slate-50"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
                />
              </svg>
            </button>
          </div>
        </div>
        <div v-else class="flex flex-1 gap-x-2 items-center justify-between">
          <input
            class="w-full flex-1 bg-transparent flex outline-none border border-white px-2 text-white rounded items-center h-9"
            v-model="editedTodo"
            @keyup.enter="updateTodo"
            @blur="cancelEdit"
          />
          <button @click="updateTodo">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0l3.181 3.183a8.25 8.25 0 0013.803-3.7M4.031 9.865a8.25 8.25 0 0113.803-3.7l3.181 3.182m0-4.991v4.99"
              />
            </svg>
          </button>
          <button @click="cancelEdit">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
      editedTodo: "",
      editIndex: -1,
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push(this.newTodo.trim());
        this.newTodo = "";
      }
    },
    editTodo(index) {
      this.editIndex = index;
      this.editedTodo = this.todos[index];
    },
    updateTodo() {
      if (this.editedTodo.trim() !== "") {
        this.todos[this.editIndex] = this.editedTodo.trim();
        this.editIndex = -1;
        this.editedTodo = "";
      }
    },
    cancelEdit() {
      this.editIndex = -1;
      this.editedTodo = "";
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.cancelEdit();
    },
  },
};
</script>
