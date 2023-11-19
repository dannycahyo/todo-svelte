<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import type { Todo } from "../types/Todo";

  const dispatch = createEventDispatcher<{
    removeTodo: string;
    toggleTodo: Pick<Todo, "id" | "completed">;
    editTodo: Todo;
  }>();

  export let todo: Todo;
  let isEditMode = false;

  function handleToggleTodo(event: Event) {
    const target = event.target as HTMLInputElement;
    dispatch("toggleTodo", {
      id: todo.id,
      completed: target.checked,
    });
  }

  function handleEditMode() {
    isEditMode = !isEditMode;
  }
</script>

{#if isEditMode}
  <div class="todo-item">
    <div class="edit-todo">
      <input type="text" bind:value={todo.title} />
      <input type="text" bind:value={todo.description} />
    </div>
    <div class="todo-item__actions">
      <button
        on:click={() => {
          dispatch("editTodo", {
            ...todo,
            title: todo.title,
            description: todo.description,
          });
          handleEditMode();
        }}>Save</button
      >
      <button on:click={handleEditMode}>Cancel</button>
    </div>
  </div>
{:else}
  <div class="todo-item">
    <div class="todo-item__title">
      <h3>{todo.title}</h3>
      <div>
        <label for="completed"
          >{todo.completed ? "Completed" : "Not Completed"}</label
        >
        <input
          type="checkbox"
          bind:checked={todo.completed}
          on:change={handleToggleTodo}
        />
      </div>
    </div>
    <div class="todo-item__description">
      <p>{todo.description}</p>
    </div>
    <div class="todo-item__actions">
      <button on:click={() => dispatch("removeTodo", todo.id)}>Remove</button>
      <button on:click={handleEditMode}>Edit</button>
    </div>
  </div>
{/if}

<style>
  .todo-item {
    margin: 1rem;
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }
  .todo-item__title {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .todo-item__title h3 {
    margin: 0;
  }
  .todo-item__description {
    margin: 0.5rem 0;
    text-align: left;
  }
  .todo-item__actions {
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }
  .todo-item__actions button {
    margin-left: 0.5rem;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }
  .edit-todo {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin-bottom: 1rem;
  }
  .edit-todo input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }

  @media (max-width: 425px) {
    .todo-item__title {
      flex-direction: column;
      gap: 0.5rem;
    }
  }
</style>
