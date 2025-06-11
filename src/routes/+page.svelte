<script>
  import Header from "$lib/Header.svelte"
  let tasks = []

  function addTask() {
    tasks = [...tasks, ""]
  }
  function removeTask(index) {
    tasks = [...tasks.slice(0, index), ...tasks.slice(index + 1)]
  }
</script>

<Header />

<main class="content section">
  <button on:click={addTask}>📝 Add</button>
  {#each tasks as task, index}
    <div class="task">
      <input bind:value={tasks[index]} />
    </div>
  {/each}
  <button
    on:click={() => {
      removeTask(index)
    }}>🗑</button
  >
</main>

<footer class="footer">
  <p class="has-text-centered">&copy; Craighead Diocesan School 2025</p>
</footer>

<style>
  .task {
    display: block;
  }
</style>
