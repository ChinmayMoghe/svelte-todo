<script>
  import Todos from "./Todos.svelte";
  let todos = [
    { id: 1, name: "Create a svelte app", completed: false },
    { id: 2, name: "Create your first svelte component", completed: true },
    { id: 3, name: "Publish on netlify", completed: false },
  ];
</script>

<Todos {todos} />
