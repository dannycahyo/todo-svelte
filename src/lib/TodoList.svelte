<script lang="ts">
  import AddTodo from "./AddTodo.svelte";
  import TodoItem from "./TodoItem.svelte";
  import { TODOS } from "../constants/TODOS";
  import type { Todo } from "../types/Todo";

  let todos: Todo[] = TODOS;

  const addTodo = (event: CustomEvent<Todo>) => {
    const newTodo = event.detail;
    todos = [...todos, newTodo];
  };

  const removeTodo = (event: CustomEvent<string>) => {
    const todoId = event.detail;
    todos = todos.filter((todo) => todo.id !== todoId);
  };

  const toggleTodo = (
    event: CustomEvent<{ id: string; completed: boolean }>,
  ) => {
    const { id, completed } = event.detail;

    todos = todos.map((todo) => {
      if (todo.id === id) {
        return {
          ...todo,
          completed,
        };
      }
      return todo;
    });
  };

  const editTodo = (event: CustomEvent<Todo>) => {
    const editedTodo = event.detail;
    todos = todos.map((todo) => {
      if (todo.id === editedTodo.id) {
        return editedTodo;
      }
      return todo;
    });
  };
</script>

<div class="card">
  <AddTodo on:addTodo={addTodo} />
</div>
{#if todos.length === 0}
  <div class="card">
    <h3>No Todos Found</h3>
  </div>
{:else}
  <div>
    {#each todos as todo (todo.id)}
      <TodoItem
        {todo}
        on:removeTodo={removeTodo}
        on:toggleTodo={toggleTodo}
        on:editTodo={editTodo}
      />
    {/each}
  </div>
{/if}

<style>
  .card {
    margin: 1rem;
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }
</style>
