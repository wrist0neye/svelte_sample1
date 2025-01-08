<!-- <script>
  import ResizableTable from "../Components/ResizableTable.svelte";
</script>

<style>
  .sketch_book {
    position: relative;
    width: 100%;
    height: 100vh;
    background-color: #f1f1f1;
    border-radius: 5px;
    padding: 8px;
  }
</style>


<div class="sketch_book">
  <ResizableTable></ResizableTable>
  <ResizableTable></ResizableTable>
</div> -->

<!-- 위 코드는 메인으로 사용할 코드 -->

<script>
  let todos = $state([
    {done: false, text: 'finish Svelte tutorial'},
    {done: false, text: 'build an app'},
    {done: false, text: 'world domination'}
  ]);

  function add() {
    todos.push({
      done: false,
      text: ''
    })
  }

  function clear() {
    todos = todos.filter((t)=> !t.done);
  }

  let remaining = $derived(todos.filter((t)=> !t.done).length);
</script>

<div class="centered">
  <h1>todos</h1>

  <ul class="todos">
    {#each todos as todo}
      <li class={{ done: todo.done}}>
        <input type="checkbox" bind:checked={todo.done}/>
        <input 
          type="text"
          placeholder="What needs to be done?"
          bind:value={todo.text}/>
      </li>
    {/each}
  </ul>

  <p>{remaining} remaining</p>

  <button onclick={add}>
    Add new
  </button>

  <button onclick={clear}>
    Clear completed
  </button>
</div>

<style>
  .centerd{
    max-width: 20em;
    margin: 0 auto;
  }

  .done {
    opacity: 0.4;
  }

  li {
    display: flex;
  }

  input[type="text"] {
    flex: 1;
    padding: 0.5em;
    margin: -0.2em 0;
    border: none;
  }
</style>