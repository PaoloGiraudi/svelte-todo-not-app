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

<div class="todo-not-item">
  <div class="todo-not-item-left" transition:fly={{ y: 20, duration: 300 }}>
    <input
      type="checkbox"
      bind:checked={completed}
      on:change={toggleComplete}
    />
    <div class="todo-not-item-label" class:completed>{title}</div>
  </div>
  <div class="remove-item" on:click={deleteTodoNot}>x</div>
</div>

<style>
  .todo-not-item {
    margin-bottom: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    animation-duration: 0.3s;
  }
  .remove-item {
    cursor: pointer;
    margin-left: 15px;
  }
  .remove-item:hover {
    color: lightseagreen;
  }
  .todo-not-item-left {
    display: flex;
    align-items: center;
  }
  .todo-not-item-label {
    border: 1px solid white;
    margin-left: 12px;
  }
  .completed {
    text-decoration: line-through;
    color: grey;
  }
</style>
