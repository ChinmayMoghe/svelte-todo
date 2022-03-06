<script>
  //   Custom event implementation - props down, events-up pattern
  //   pass down props from parent to child , bubble up event from child to parent, capture
  //   event in parent

  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  export let todo;
  let editing = false;
  let name = todo.name;
  function update(updatedTodo) {
    todo = { ...todo, ...updatedTodo };
    dispatch("update", todo);
  }
  const onCancel = () => {
    name = todo.name;
    editing = false;
  };
  const onSave = () => {
    update({ name: name });
    editing = false;
  };
  const onRemove = () => {
    dispatch("remove", todo);
  };
  const onEdit = () => (editing = true);
  const toggleTodo = () => update({ completed: !todo.completed });
</script>

{#if editing}
  <form
    on:submit|preventDefault={onSave}
    on:keydown={(e) => e.key === "Escape" && onCancel()}
    class="edit_todo"
  >
    <label for="task-1">New description for {name}</label>
    <input
      type="text"
      name="task-1"
      id="task-1"
      placeholder="Update description"
      bind:value={name}
      autocomplete="off"
    />
    <div class="btn_group">
      <button on:click={onCancel}>
        <span>Cancel</span>
        <span class="sr-only">renaming {name}</span></button
      >
      <button type="submit" disabled={!name}>
        <span>Save</span>
        <span class="sr-only">new name for {name}</span></button
      >
    </div>
  </form>
{:else}
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
      <button on:click={onEdit}>
        <span>Edit</span>
        <span class="sr-only">{todo.name}</span>
      </button>
      <button on:click={() => dispatch("remove", todo)}>
        <span>Delete</span>
        <span class="sr-only">{todo.name}</span>
      </button>
    </div>
  </form>
{/if}

<style>
  .edit_todo {
    display: flex;
    flex-direction: column;
  }
</style>
