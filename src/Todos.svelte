<div class="todo_app">
  <div class="card">
    <form>
      <h1>
        <label for="task-input">Get things done !!!</label>
      </h1>
      <input
        type="text"
        name="task-input"
        id="task-input"
        placeholder="Enter task description here"
      />
      <button type="submit">Add Task</button>
    </form>
    <div>
      <button>
        <span>Show</span><span>All</span><span>Tasks</span>
      </button>
      <button>
        <span>Show</span><span>Active</span><span>Tasks</span>
      </button>
      <button>
        <span>Show</span><span>Completed</span><span>Tasks</span>
      </button>
    </div>
    <h2>2 out of 3 items completed</h2>

    <ul>
      <li>
        <form>
          <label for="task-1"
            >New description for 'Create a svelte todo list app'</label
          >
          <input type="text" name="task-1" id="task-1" />
          <button>
            <span>Cancel</span>
            <span>renaming 'Create a svelte todo list app'</span></button
          >
          <button>
            <span>Save</span>
            <span>new name for 'Create a svelte todo list app'</span></button
          >
        </form>
      </li>
      <li>
        <form>
          <input type="checkbox" name="task-2" id="task-2" />
          <label for="task-2">Create your first component</label>
          <button
            ><span>Edit</span>
            <span>Create your first component</span></button
          >
          <button
            ><span>Delete</span>
            <span>Create your first component</span></button
          >
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
  }
  .card {
    background-color: #fff;
    color: #333;
    border-radius: 12px;
    padding: 15px;
  }
</style>
