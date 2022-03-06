<script>
  export let filter = "all";
  const applyFilter = (appliedFilter) => {
    filter = appliedFilter;
  };
</script>

<div class="btn_group">
  <button on:click={() => applyFilter("all")}>
    <span class="sr-only">Show</span>
    <span>All</span>
    <span class="sr-only">Tasks</span>
  </button>
  <button on:click={() => applyFilter("active")}>
    <span class="sr-only">Show</span>
    <span>Active</span>
    <span class="sr-only">Tasks</span>
  </button>
  <button on:click={() => applyFilter("completed")}>
    <span class="sr-only">Show</span>
    <span>Completed</span>
    <span class="sr-only">Tasks</span>
  </button>
</div>
