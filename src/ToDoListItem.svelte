<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import type { ToDoData } from './data';

	export let TD: ToDoData;
	const dispatch = createEventDispatcher();
	const closeHandler = () => dispatch('deleteLI', TD);
    let formDisplay:string = "hideElement";
    let dataDisplay:string = "showElement";
    function editLIStartProcess(){
        formDisplay = "showElement";
        dataDisplay = "hideElement";
    }

    function editLIFinalization(){
        formDisplay = "hideElement";
        dataDisplay = "showElement";
    }
	
</script>

<li>
	<span class={dataDisplay} id="nameSpan">{TD.name}</span>
	<span class={dataDisplay} id="descriptionSpan">{TD.description}</span>
	<span class={dataDisplay} id="prioritySpan">{TD.priority}</span>
	<form class={formDisplay}>
		<input type="text" placeholder="toDo Name" bind:value={TD.name} />
		<input type="text" placeholder="toDo Description" bind:value={TD.description}/>
		<input type="number" placeholder="toDo Priority" bind:value={TD.priority} />
        <button type="submit" id="editSubmitButton" on:click|preventDefault={() => editLIFinalization()}>submit edit</button>
	</form>

	<button on:click|preventDefault={closeHandler}>delete</button>
	<button on:click|preventDefault={() => editLIStartProcess()}>edit</button>

</li>

<style>
	.hideElement {
		display: none;
	}
    .showElement{
        display: inline;
    }
</style>
