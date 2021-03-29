<script>
  import TodoNotItem from "./TodoNotItem.svelte";

  let newTodoNotTitle = "";
  let currentFilter = "all";
  let nextId = 4;

  let todosNot = [
    {
      id: 1,
      title: "I will not do",
      completed: false,
    },
    {
      id: 2,
      title: "I will still not do",
      completed: false,
    },
    {
      id: 3,
      title: "I will never do",
      completed: false,
    },
  ];


</script>

<div class="container">
  <img src={"/img/dont-cross.png"} alt="dont cross" />
  <h2>Svelte Todo NOT App.</h2>
  <input
    type="text"
    class="todoNot-input"
    placeholder="Today I will NOT..."
    bind:value={newTodoNotTitle}
    on:keydown={addTodoNot}
  />

  {#each filteredTodosNot as item}
    <div class="todo-not-item">
      <TodoNotItem
        {...todoNot}
        on:deleteTodoNot={handleDeleteItem}
        on:toggleComplete={handleToggleComplete}
      />
    </div>
  {/each}

  <div class="inner-container">
    <div>
      <label>
        <input
          type="checkbox"
          class="inner-container-input"
          on:change={checkAllTodosNot}
        /> Check All
      </label>
    </div>
    <div>{todosNotRemaining} items left</div>
  </div>

  <div class="inner-container">
    <div>
      <button
        on:click={() => updateFilter("all")}
        class:active={currentFilter === "all"}>All</button
      >
    </div>
    <div>
      <button
        on:click={() => updateFilter("active")}
        class:active={currentFilter === "active"}>Active</button
      >
    </div>
    <div>
      <button
        on:click={() => updateFilter("completed")}
        class:active={currentFilter === "completed"}>Completed</button
      >
    </div>
    <div>
      <button on:click={clearCompleted}>Clear Completed</button>
    </div>
  </div>
</div>
