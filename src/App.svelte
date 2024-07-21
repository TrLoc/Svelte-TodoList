<script>
  let todos = [
    { done: false, text: "clean the room" },
    { done: false, text: "read a book" },
    { done: false, text: "exercise" },
  ];

  function add() {
    todos = todos.concat({
      done: false,
      text: "",
    });
  }

  function clear() {
    todos = todos.filter((t) => !t.done);
  }

  $: remaining = todos.filter((t) => !t.done).length;
</script>

<div class="centered">
  <h1>todos</h1>

  <ul class="todos">
    {#each todos as todo}
      <li class:done={todo.done}>
        <input type="checkbox" bind:checked={todo.done} />

        <input
          type="text"
          placeholder="What needs to be done?"
          bind:value={todo.text}
        />
      </li>
    {/each}
  </ul>

  <p>{remaining} remaining</p>

  <button on:click={add}> Add new </button>

  <button on:click={clear}> Clear completed </button>
</div>

<style>
  .centered {
    max-width: 20em;
    margin: 0 auto;
  }

  .done {
    opacity: 0.6;
  }

  li {
    display: flex;
    margin-bottom: 10px;
  }

  input[type="text"] {
    flex: 1;
    padding: 0.5em;
    margin: -0.2em 0;
    border: none;
  }
</style>
