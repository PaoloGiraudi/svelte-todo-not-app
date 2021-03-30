<script>
  import { createEventDispatcher } from "svelte";
  import { fly } from "svelte/transition";

  export let id;
  export let title;
  export let completed;

  const dispatch = createEventDispatcher();

  function deleteTodoNot() {
    dispatch("deleteTodoNot", {
      id: id,
    });
  }

  function toggleComplete() {
    dispatch("toggleComplete", {
      id: id,
    });
  }
</script>

<div class="todo-not-container">
  <div class="todo-not-item" transition:fly={{ y: 20, duration: 300 }}>
    <div class="icon" on:click={toggleComplete}>
      {#if completed}
        ✔️
      {:else}
        🔲
      {/if}
    </div>
    <div class="label" class:completed>{title}</div>
  </div>
  <div class="icon" on:click={deleteTodoNot}>❌</div>
</div>

<style>
  .todo-not-container {
    margin: 1em 0.5em;
    padding: 0.25em;
    display: flex;
    align-items: center;
    justify-content: space-between;
    animation-duration: 0.3s;
  }
  .icon {
    cursor: pointer;
  }

  .todo-not-item {
    display: flex;
    align-items: center;
  }
  .label {
    border: 1px solid white;
    margin-left: 12px;
  }
  .completed {
    text-decoration: line-through;
    color: grey;
  }
</style>
