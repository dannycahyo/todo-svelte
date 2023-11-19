<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import TodoList from "./lib/TodoList.svelte";
</script>

<main>
  <div class="heroes-container">
    <h1>Svelte CRUD Todo List</h1>
    <div>
      <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
        <img src={viteLogo} class="logo" alt="Vite Logo" />
      </a>
      <a href="https://svelte.dev" target="_blank" rel="noreferrer">
        <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
      </a>
    </div>
  </div>
  <div class="todo-container">
    <TodoList />
  </div>
</main>

<style>
  main {
    height: 100vh;
  }

  .heroes-container {
    display: flex;
    gap: 2rem;
    align-items: center;
  }

  .todo-container {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  @media (max-width: 768px) {
    .todo-container {
      flex-direction: column;
    }
    .heroes-container {
      flex-direction: column;
      gap: 0;
    }
    h1 {
      text-align: center;
      font-size: x-large;
    }
  }
</style>
