<script>
	// let firstName = 'Chuck'
	// let lastName = 'Spadina'
	// let beltColor = 'black'

	// $: fullName = `${firstName} ${lastName}`
	// $: {
	// 	console.log(beltColor)
	// 	console.log(fullName)
	// }

	// const handleClick = () => {
	// 	beltColor = 'orange'
	// }
	// const handleInput = (e) => {
	// 	beltColor = e.target.value
	// }
	
	import Modal from './Modal.svelte'
	import AddPersonForm from './AddPersonForm.svelte'

	let showModal = false

	let people = [
		{ name : 'Kobayashi', beltColour: 'black', age: 25, id:1 },
		{ name : 'Takeshi', beltColour: 'orange', age: 45, id:2 },
		{ name : 'Shin Jo', beltColour: 'brown', age: 35, id:3 },
	]
	const handleClick = (id) => {
		people = people.filter(person => person.id !== id)
	}

	const handleModal = () => {
		showModal = !showModal
	}

	const addPerson = (e) => {
		// console.log(e.detail);
		const person = e.detail
		people = [person, ...people]
		showModal = false
	}

</script>

<Modal {showModal} on:click={handleModal}>
	
	<AddPersonForm on:addPerson = {addPerson}/>
	<!-- <div slot='title'>
		<h3>Add a new person</h3>
	</div> -->
</Modal>

<!-- <Modal message= " Hey, again " /> -->

<main>
	
	<!-- <p>{fullName} - {beltColor} belt</p>
	<input type="text" bind:value={firstName}>
	<input type="text" bind:value={lastName}>
	<input type="text" bind:value={beltColor}> -->

	<button on:click= {handleModal}>Add Person</button>

	{#each people as person (person.id) }
		<div>
			<h4>{person.name}</h4>
			{#if person.beltColour === 'black'} 
				<p><strong> MASTER NINJA </strong></p>
			{/if}
			<p>{person.age} years old, {person.beltColour} </p>
			{#if person.skills}
				<p>Skills:</p>
				{#each person.skills as skill }
					<p>{skill}</p>
				{/each}
			{/if}

			<button on:click={() => handleClick(person.id) }> delete </button>
		</div>
		{:else}
			<p>There are no people</p>	
	{/each}

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	/* h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	} */

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>