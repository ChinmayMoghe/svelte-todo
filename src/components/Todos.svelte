<script>
  import Filter from "./Filter.svelte";
  import Todo from "./Todo.svelte";
  export let todos = [];
  $: totalTodos = todos.length;
  $: completedTodos = todos.filter((todo) => todo.completed).length;

  let newTodoName = "";

  function addTodo() {
    todos = [
      ...todos,
      { id: Math.random(), name: newTodoName, completed: false },
    ];
    newTodoName = "";
  }

  let filter = "all";

  const filterTodos = (filter, todos) =>
    filter === "active"
      ? todos.filter((t) => !t.completed)
      : filter === "completed"
      ? todos.filter((t) => t.completed)
      : todos;

  function removeTodo(todo) {
    todos = todos.filter((t) => t.id !== todo.id);
  }

  const updateTodo = (todo) => {
    console.log("update todo event", todo);
    todos = todos.map((td) => {
      if (td.id === todo.id) {
        td = { ...td, ...todo };
      }
      return td;
    });
  };
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
      <button type="submit" disabled={!newTodoName}>Add Task</button>
    </form>
    <!--Add filter button component here-->
    <Filter bind:filter />
    <h2>{completedTodos} out of {totalTodos} items completed</h2>
    <ul>
      {#each filterTodos(filter, todos) as todo, index (todo.id)}
        <li key={index}>
          <!--Todo component custom event-->
          <Todo
            {todo}
            on:remove={(e) => removeTodo(e.detail)}
            on:update={(e) => updateTodo(e.detail)}
          />
        </li>
      {:else}
        <li>Nothing to do here !!!!</li>
        <li />{/each}
    </ul>

    <ul>
      <li>
        <!--TODO: Remove this code: <ul>-->
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

  ul > li {
    margin: 10px 0;
  }
</style>
