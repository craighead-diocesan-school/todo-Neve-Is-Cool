<script>
  import Header from "$lib/Header.svelte"
  let tasks = []

  function addTask() {
    tasks = [...tasks, ""]
    saveTasks()
  }
  function removeTask(index) {
    tasks = [...tasks.slice(0, index), ...tasks.slice(index + 1)]
    saveTasks()
  }
  function saveTasks() {
    localStorage.todos = JSON.stringify(tasks)
  }
  function loadTasks() {
    tasks = JSON.parse(localStorage.todos)
  }
  let showLabel = false
  let answer = "yes"
</script>

<Header />

<main class="content section">
  <button on:click={addTask}>📝 Add</button>
  <button on:click={saveTasks}>💾 Save</button>
  <button on:click={() => (showLabel = true)}>📡 Load</button>

  {#if showLabel}
    <label>
      Load Tasks?
      <select bind:value={answer}>
        <option value="yes">Yes</option>
        <option value="no">No</option>
      </select>
      <button
        on:click={() => {
          loadTasks()
          showLabel = false
        }}>Confirm</button
      >
    </label>
  {/if}

  {#each tasks as task, index}
    <div class="task">
      <input bind:value={tasks[index]} />
      <button
        on:click={() => {
          removeTask(index)
        }}>🗑</button
      >
    </div>
  {/each}
</main>

<footer class="footer">
  <p class="has-text-centered">&copy; Craighead Diocesan School 2025</p>
</footer>

<style>
  .task {
    display: block;
    margin: 0.5rem;
  }

  input {
    padding: 0.5rem;
  }

  button {
    border: #000 solid 1px;
    padding: 0.5rem;
  }
</style>
