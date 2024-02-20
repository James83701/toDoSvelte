<script lang="ts">
	import ToDoListItem from '../ToDoListItem.svelte';
import type { ToDoData } from '../data';
	import ToDoHeader from '../toDoHeader.svelte';
	let toDoTitle: string = '';
	let toDoDescription: string = '';
	let toDoPriority: number | null;
	let listOfTD: ToDoData[] = [];

	function storeTitle() {
		if (toDoPriority != null) {
			let newTD: ToDoData = {
				name: toDoTitle,
				description: toDoDescription,
				priority: toDoPriority,
                index: 0
			};
            listOfTD = [...listOfTD, newTD];
            indexRefresh();
            toDoTitle = "";
            toDoDescription = "";
            toDoPriority = 0;
		}

		
        
	}

    function deleteLI(TD: ToDoData){
        console.table(listOfTD);
        let index = TD.index;
        console.log(index);
        listOfTD = listOfTD.filter((_, i) => i !== index);
        indexRefresh();
        console.table(listOfTD);
    }

    function indexRefresh(){
        for (let index = 0; index < listOfTD.length; index++) {
            let TD:ToDoData = listOfTD[index];
            TD.index = index;
        }
    }

    
</script>

<ToDoHeader name="john" />
<p>make a new toDo:</p>
<form id="newToDoForm">
	<input type="text" placeholder="toDo Name" bind:value={toDoTitle} />
	<input type="text" placeholder="toDo Description" bind:value={toDoDescription} />
	<input type="number" placeholder="toDo Priority" bind:value={toDoPriority} />
	<button type="submit" id="newToDoSubmitButton" on:click|preventDefault={storeTitle}>submit</button
	>
</form>

<ul id="listDisplay">Things To Do:</ul>

{#each listOfTD as TD}
    <ToDoListItem TD={TD} on:deleteLI = {() => deleteLI(TD)}></ToDoListItem>
{/each}
