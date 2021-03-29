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

