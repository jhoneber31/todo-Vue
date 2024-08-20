<template>
  <div class="container mx-auto my-10">
    <h1 class="text-center text-3xl font-semibold mb-4">To Do List</h1>
    <div class="md:w-1/2 mx-auto">
      <div class="bg-white shadow-md rounded-lg p-6">
        <form id="todo-form" @submit.prevent="addTodo">
          <div class="flex mb-4">
            <input
              type="text"
              class="w-full px-4 py-2 mr-2 border-b border-gray-300 focus:outline-none focus:border-blue-500"
              id="todo-input"
              v-model="newTodo"
              placeholder="Add new task"
              required
            />
            <button
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
              type="submit"
            >
              {{ editingIndex !== null ? "Update" : "Add" }}
            </button>
          </div>
        </form>

        <div v-if="todos.length === 0" class="mt-5">
          <p class="text-center text-gray-400">No tasks found</p>
        </div>

        <table v-else class="min-w-full">
          <thead class="bg-white border-b">
            <tr>
              <th
                scope="col"
                class="text-sm font-medium text-gray-900 px-6 py-4 text-center w-1/12"
              >
                #
              </th>
              <th
                scope="col"
                class="text-sm font-medium text-gray-900 px-6 py-4 text-center w-7/12"
              >
                Task
              </th>
              <th
                scope="col"
                class="text-sm font-medium text-gray-900 px-6 py-4 text-center w-2/12"
              >
                Edit
              </th>
              <th
                scope="col"
                class="text-sm font-medium text-gray-900 px-6 py-4 text-center w-2/12"
              >
                Delete
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              :class="index % 2 === 0 ? 'bg-gray-100' : 'bg-white'"
              class="border-b"
              v-for="(todo, index) in todos"
              :key="index"
            >
              <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 text-center">
                {{ index + 1 }}
              </td>
              <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 text-center">
                {{ todo }}
              </td>
              <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 text-center">
                <div class="flex justify-center">
                  <img src="../assets/edit-icon.svg" alt="edit-icon" width="20" @click="editTodo(index)" class="cursor-pointer">
                </div>
              </td>
              <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 text-center">
                <div class="flex justify-center">
                  <img src="../assets/delete-icon.svg" alt="delete-icon" width="20" @click="removeTodo(index)" class="cursor-pointer">
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script lang="ts">


export default {
  data() {
    return {
      newTodo: "" as string,
      todos: [] as string[],
      editingIndex: null as number | null,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length === 0) return;

      if (this.editingIndex !== null) {
        this.todos[this.editingIndex] = this.newTodo;
        this.editingIndex = null;
      } else {
        this.todos.push(this.newTodo);
      }
      this.newTodo = "";
    },
    removeTodo(index: number) {
      this.todos.splice(index, 1);
    },
    editTodo(index: number) {
      this.newTodo = this.todos[index];
      this.editingIndex = index;
    },
  },
};
</script>
