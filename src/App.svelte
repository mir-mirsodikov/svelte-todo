<script lang="ts">
  import { onMount } from "svelte";
  import Todo from "./lib/Todo.svelte";

  type Todo = {
    id: number;
    completed: boolean;
    todo: string;
  };

  let todos: Todo[] = [];
  let errMessage: string = "";

  onMount(() => {
    const todosFromLocalStorage = localStorage.getItem("todos");

    if (todosFromLocalStorage) {
      todos = JSON.parse(todosFromLocalStorage);
    }
  });

  let newTodo: string = "";

  const updateLocalStorage = () => {
    localStorage.setItem("todos", JSON.stringify(todos));
  };

  const addTodo = () => {
    if (newTodo === "") {
      errMessage = "Please enter a todo";
      return;
    }
    
    errMessage = "";
    const id = (todos[todos.length - 1]?.id ?? 0) + 1;
    todos = [
      ...todos,
      {
        id,
        completed: false,
        todo: newTodo,
      },
    ];

    newTodo = "";
    updateLocalStorage();
  };

  const toggleTodo = (id: number) => {
    todos = todos.map((todo) => {
      if (todo.id === id) {
        return {
          ...todo,
          completed: !todo.completed,
        };
      }
      return todo;
    });
    updateLocalStorage();
  }

  const removeTodo = (id: number) => {
    todos = todos.filter((todo) => todo.id !== id);
    updateLocalStorage();
  };
</script>

<main class="mt-4">
  <h1 class="text-center text-4xl font-bold mb-4">Todo</h1>
  <div class="flex flex-col w-1/2 bg-white rounded-lg shadwo-md border m-auto p-4">
    <input
      class="border rounded-md h-8"
      type="text"
      placeholder="Add Todo"
      bind:value={newTodo}
    />
    {#if errMessage}
      <p class="text-red-500">{errMessage}</p>
    {/if}
    <button
      class="border rounded-md bg-slate-800 text-white p-4 w-40 hover:bg-slate-700 mt-4"
      on:click={addTodo}>Add</button
    >
  </div>

  <div class="w-1/2 m-auto mt-8">
    <h1 class="text-3xl font-bold border">Active Todos</h1>
    {#each todos as todo (todo.id)}
      {#if !todo.completed}
        <Todo
          {...todo}
          on:toggle={(event) => toggleTodo(event.detail)}
          on:remove={(event) => removeTodo(event.detail)}
        />
      {/if}
    {/each}
  </div>

  <div class="w-1/2 m-auto mt-8">
    <h1 class="text-3xl font-bold border">Completed Todos</h1>
    {#each todos as todo (todo.id)}
      {#if todo.completed}
        <Todo
          {...todo}
          on:toggle={(event) => toggleTodo(event.detail)}
          on:remove={(event) => removeTodo(event.detail)}
        />
      {/if}
    {/each}
  </div>
</main>
