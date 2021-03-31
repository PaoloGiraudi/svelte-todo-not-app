<script>
  import TodoNotItem from "./TodoNotItem.svelte";

  let newTodoNotTitle = "";
  let currentFilter = "all";
  let nextId = 4;

  // Array of objects to store the items

  let todosNot = [
    {
      id: 1,
      title: "Paint my house yellow",
      completed: false,
    },
    {
      id: 2,
      title: "Crash into a bus with my bike",
      completed: false,
    },
    {
      id: 3,
      title: "Forget sunscreen",
      completed: false,
    },
  ];

  function addTodoNot(event) {
    if (event.key === "Enter") {
      todosNot = [
        ...todosNot,
        {
          id: nextId,
          title: newTodoNotTitle,
          completed: false,
        },
      ];

      nextId++;
      newTodoNotTitle = "";
    }
  }

  $: todosNotRemaining = filteredTodosNot.filter((t) => !t.completed).length;
  $: filteredTodosNot =
    currentFilter === "all"
      ? todosNot
      : currentFilter === "completed"
      ? todosNot.filter((t) => t.completed)
      : todosNot.filter((t) => !t.completed);

  function checkAllTodosNot(event) {
    todosNot.forEach((t) => (t.completed = event.target.checked));
    todosNot = todosNot;
  }

  function updateFilter(newFilter) {
    currentFilter = newFilter;
  }

  function clearCompleted() {
    todosNot = todosNot.filter((t) => !t.completed);
  }

  function handleDeleteItem(event) {
    todosNot = todosNot.filter((t) => t.id !== event.detail.id);
  }

  function handleToggleComplete(event) {
    const index = todosNot.findIndex((t) => t.id === event.detail.id);
    const updatedTodoNot = {
      ...todosNot[index],
      completed: !todosNot[index].completed,
    };

    todosNot = [
      ...todosNot.slice(0, index),
      updatedTodoNot,
      ...todosNot.slice(index + 1),
    ];
  }
</script>

<div class="app-container">
  <header>
    <div class="tape" />
    <h1>Svelte Todo NOT App</h1>
    <div class="tape" />
  </header>
  <input
    type="text"
    class="todo-not-input"
    placeholder="Today I will NOT..."
    bind:value={newTodoNotTitle}
    on:keydown={addTodoNot}
  />

  {#each filteredTodosNot as todosNot}
    <div class="todo-not-item">
      <TodoNotItem
        {...todosNot}
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
          class="inner-container-text"
          on:change={checkAllTodosNot}
        /> Check All
      </label>
    </div>
    <div class="inner-container-text">{todosNotRemaining} items left</div>
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

<style>
  .app-container {
    max-width: 800px;
    margin: 10px auto;
  }

  .tape {
    height: 1rem;
    width: 100%;
    background: rgb(0, 0, 0);
    background: linear-gradient(
      45deg,
      rgba(0, 0, 0, 1) 10%,
      rgba(255, 231, 0, 1) 10%,
      rgba(255, 231, 0, 1) 20%,
      rgba(0, 0, 0, 1) 20%,
      rgba(0, 0, 0, 1) 30%,
      rgba(255, 231, 0, 1) 30%,
      rgba(255, 231, 0, 1) 40%,
      rgba(0, 0, 0, 1) 40%,
      rgba(0, 0, 0, 1) 50%,
      rgba(255, 231, 0, 1) 50%,
      rgba(255, 231, 0, 1) 60%,
      rgba(0, 0, 0, 1) 60%,
      rgba(0, 0, 0, 1) 70%,
      rgba(255, 231, 0, 1) 70%,
      rgba(255, 231, 0, 1) 80%,
      rgba(0, 0, 0, 1) 80%,
      rgba(0, 0, 0, 1) 90%,
      rgba(255, 231, 0, 1) 90%
    );
  }

  h1 {
    text-align: center;
  }
  .todo-not-input {
    margin: 1rem 0.5rem;
    margin-bottom: 0;
    padding: 0.5rem;
  }
  .inner-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 1rem 0.5rem;
    border-top: 1px solid lightgrey;
  }
  .inner-container-text {
    padding: 1em 0.5em;
  }
  button {
    display: inline-block;
    font-size: 1rem;
    cursor: pointer;
    border: none;
    background-color: rgb(199, 194, 194);
    margin-top: 1rem;
    padding: 0.5em 1em;
  }
  button:hover {
    background: rgba(255, 231, 0, 1);
  }
  button:focus {
    outline: none;
  }
  .active {
    background: rgba(255, 231, 0, 1);
  }
</style>
