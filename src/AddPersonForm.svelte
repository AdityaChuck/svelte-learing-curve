<script>
    
    import { createEventDispatcher } from 'svelte'

    let dispatch = createEventDispatcher()

    let name
    let beltColour
    let age
    let skills = []
    const handleSubmit = () => {
        const person = {
            name,
            beltColour,
            age,
            skills,
            id: new Date() % 10000
        }

        dispatch('addPerson', person)
    }
    
</script>

<form on:submit|preventDefault={handleSubmit} >
    <input type="text" placeholder='name' bind:value = {name}>
    <br/>
    <label for="selectId"> Belt Color:</label>
    <select id="selectId" bind:value={beltColour}>
        <option value="black">black</option>
        <option value="orange">orange</option>
        <option value="brown">brown</option>
        <option value="white">white</option>
    </select>
    <br/>
    <input type="number" placeholder="age" bind:value = {age}>
    <label for="skills">Skils: </label>
    <input id="skills" type="checkbox" bind:group= {skills} value="fighting">&nbsp;fighting<br/>
    <input id="skills" type="checkbox" bind:group= {skills} value="sneaking">&nbsp;sneaking<br/>
    <input id="skills" type="checkbox" bind:group= {skills} value="running">&nbsp;running<br/>
    <button>Add Person</button>
</form>

<style></style>