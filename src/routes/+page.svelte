<script>
  import Header from "$lib/Header.svelte"
  let tasks = []

  // Check if localStorage has tasks, if not initialize it
  function addTask() {
    tasks = [...tasks, ""]
    saveTasks()
  }

  // Remove a task by index
  // and save the updated tasks to localStorage
  function removeTask(index) {
    tasks = [...tasks.slice(0, index), ...tasks.slice(index + 1)]
    saveTasks()
  }
  function saveTasks() {
    localStorage.todos = JSON.stringify(tasks)
  }

  // Load tasks from localStorage if available
  function loadTasks() {
    tasks = JSON.parse(localStorage.todos)
  }
  let showLabel = false
  let answer = "yes"
</script>

<Header />

<main class="content section">
  <section class="buttons">
    <button class="button" on:click={addTask}>📝 Add</button>
    <button class="button" on:click={saveTasks}>💾 Save</button>
    <button class="button" on:click={() => (showLabel = true)}>📡 Load</button>
  </section>
  <section class="label">
    {#if showLabel}
      <label>
        Load Tasks?
        <select bind:value={answer}>
          <option value="yes">Yes</option>
          <option value="no">No</option>
        </select>
        {#if answer === "yes"}
          <button
            on:click={() => {
              loadTasks()
              showLabel = false
            }}>Confirm</button
          >
        {:else}
          <p>Tasks not loaded</p>
        {/if}
      </label>
    {/if}
  </section>

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

  .button {
    display: flex;
    flex-direction: row;
  }

  .content {
    display: flex;
    flex-direction: column;
    margin: 1rem;
  }
</style>
