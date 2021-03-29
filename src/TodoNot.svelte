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
    console.log(event);
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

<style>
  img {
    max-width: 100%;
  }
  .container {
    max-width: 800px;
    margin: 10px auto;
  }

  /* .todo-input {
    width: 100%;
    padding: 10px, 20px;
    font-size: 18px;
    margin-bottom: 20px;
  } */

  .inner-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 15px;
    margin-bottom: 13px;
  }
  .inner-container-input {
    margin-right: 12px;
  }
  button {
    font-size: 14px;
    background-color: white;
    appearance: none;
  }
  button:hover {
    background: lightseagreen;
  }
  button:focus {
    outline: none;
  }
  .active {
    background: lightseagreen;
  }
</style>
