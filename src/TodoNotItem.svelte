<script>
  import { createEventDispatcher } from "svelte";
  import { fly } from "svelte/transition";
</script>

<div class="todo-not-item">
  <div class="todo-not-item-left" transition:fly={{ y: 20, duration: 300 }}>
    <input
      type="checkbox"
      bind:checked={completed}
      on:change={toggleCompleted}
    />
    <div class="todo-not-item-label" class:completed>{title}</div>
  </div>
  <div class="remove-item" on:click={deleteTodoNot}>x</div>
</div>
