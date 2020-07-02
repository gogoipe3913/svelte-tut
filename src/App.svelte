<main>
	<div>
		NALLOW:
		<button on:click={() => {condition=null}}>ALL</button>
		<button on:click={() => {condition=false}}>LEFT</button>
		<button on:click={() => {condition=true}}>DONE</button>
	</div>
  <div>
    <input type="text" bind:value={title}>
    <button on:click={addTodo}>ADD</button>
  </div>
  <div>
    <ul>
      {#each filteredTodoList(todos, condition) as todo (todo.id)}
        <li>
          <input type="checkbox" bind:checked={todo.done}> {todo.title}
        </li>
      {/each}
    </ul>
  </div>
</main>

<script>
let title = '';
let condition = null
let todos = [
	{ id: 0, done: false, title: '欲しいものリストを作成する'},
	{ id: 1, done: false, title: '花瓶を買う'},
	{ id: 2, done: false, title: '赤いものを買う'},
]

$: filteredTodoList = (todos, condition) => {
  return condition === null ? todos : todos.filter(todo => todo.done === condition)
}
function addTodo() {
  todos = [...todos, {
    id: todos.length,
    done: false,
    title
  }];
}
</script>

<style>
li {
  list-style: none;
}
</style>