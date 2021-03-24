<script>
	export let name;
	export let todoList = [
		{id: 0, done: false, title: '定期券の購入'},
		{id: 1, done: false, title: 'トイレットペーパーの購入'},
	]
	export let currentText = ''
	export const addTask = () => {
		console.debug(todoList)
		if(currentText){
			todoList = [...todoList,
			{
				id: todoList.length,
				done: false,
				title: currentText
			}
		]
		currentText = ''
		}
	}
	let condition = null
	$: filterTodoList = () => {
		return condition === null ? todoList : todoList.filter(todo=> todo.done === condition)
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<!-- <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->
	<h2>TODO List </h2>
	<div>
		絞り込み: 
		<button on:click={()=>{condition = null}} >All</button>
		<button on:click={()=>{condition = false}}>Undone</button>
		<button on:click={()=>{condition = true}}>Done</button>
	</div>
	<div>
		<input type="text" bind:value={currentText}>
		<button on:click={addTask}>Submit</button>
	</div>
	<div>
		<ul>
			<!-- {#each todoList as todo (todo.id)} -->
			{#each filterTodoList() as todo (todo.id)}
			{#key todo.done}
			<li>
				<input type="checkbox" bind:checked={todo.done}>{todo.title}
			</li>
			{/key}
			{/each}
		</ul>
	</div>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1,h2 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 3em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>