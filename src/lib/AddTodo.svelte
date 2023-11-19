<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import type { Todo } from "../types/Todo";

  let todoTitle: string = "";
  let todoDesc: string = "";
  const dispatch = createEventDispatcher<{ addTodo: Todo }>();

  function addNewTodo() {
    dispatch("addTodo", {
      id: Math.random().toString(36).substr(2, 9),
      title: todoTitle,
      description: todoDesc,
      completed: false,
    });
    todoTitle = "";
    todoDesc = "";
  }
</script>

<div class="add-todo">
  <input type="text" bind:value={todoTitle} placeholder="Todo Title" />
  <input type="text" bind:value={todoDesc} placeholder="Todo Description" />
  <button on:click={addNewTodo}>Add Todo</button>
</div>

<style>
  .add-todo {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 1rem;
    align-items: center;
  }
  .add-todo input {
    margin: 0.5rem;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }
  .add-todo button {
    margin: 0.5rem;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }
</style>
