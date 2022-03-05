<script>
  export let todos = [];
  $: totalTodos = todos.length;
  $: completedTodos = todos.filter((todo) => todo.completed).length;
  function removeTodo(todo) {
    todos = todos.filter((t) => t.id !== todo.id);
  }

  let newTodoName = "";

  function addTodo() {
    todos = [
      ...todos,
      { id: Math.random(), name: newTodoName, completed: false },
    ];
    newTodoName = "";
  }
</script>

<div class="todo_app">
  <div class="card">
    <form on:submit|preventDefault={addTodo}>
      <h1>
        <label for="task-input">Get things done !!!</label>
      </h1>
      <input
        bind:value={newTodoName}
        type="text"
        name="task-input"
        id="task-input"
        placeholder="Enter task description here"
      />
      <button type="submit">Add Task</button>
    </form>
    <div class="btn_group">
      <button>
        <span class="sr-only">Show</span>
        <span>All</span>
        <span class="sr-only">Tasks</span>
      </button>
      <button>
        <span class="sr-only">Show</span>
        <span>Active</span>
        <span class="sr-only">Tasks</span>
      </button>
      <button>
        <span class="sr-only">Show</span>
        <span>Completed</span>
        <span class="sr-only">Tasks</span>
      </button>
    </div>
    <h2>{completedTodos} out of {totalTodos} items completed</h2>
    <ul>
      {#each todos as todo, index (todo.id)}
        <li key={index}>
          <form>
            <input
              type="checkbox"
              name="task-{todo.id}"
              id="task-{todo.id}"
              on:click={() => (todo.completed = !todo.completed)}
              checked={todo.completed}
            />
            <label for="task-{todo.id}">{todo.name}</label>
            <div class="btn_group">
              <button on:click={(event) => event.preventDefault()}>
                <span>Edit</span>
                <span class="sr-only">{todo.name}</span>
              </button>
              <button on:click={() => removeTodo(todo)}>
                <span>Delete</span>
                <span class="sr-only">{todo.name}</span>
              </button>
            </div>
          </form>
        </li>
      {:else}
        <li>Nothing to do here !!!!</li>
        <li />{/each}
    </ul>

    <ul>
      <li>
        <form class="edit_todo">
          <label for="task-1"
            >New description for 'Create a svelte todo list app'</label
          >
          <input
            type="text"
            name="task-1"
            id="task-1"
            placeholder="Update description"
          />
          <div class="btn_group">
            <button>
              <span>Cancel</span>
              <span class="sr-only"
                >renaming 'Create a svelte todo list app'</span
              ></button
            >
            <button>
              <span>Save</span>
              <span class="sr-only"
                >new name for 'Create a svelte todo list app'</span
              ></button
            >
          </div>
        </form>
      </li>
    </ul>
  </div>
</div>

<style>
  .todo_app {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 90vh;
  }
  .card {
    background-color: #fff;
    color: #333;
    border-radius: 12px;
    padding: 15px;
  }

  h1 {
    text-align: center;
  }

  .edit_todo {
    display: flex;
    flex-direction: column;
  }
  ul > li {
    margin: 10px 0;
  }

  .btn_group {
    display: flex;
  }

  .btn_group button {
    flex: 1;
  }
</style>
