<script lang="ts">
	import { LOGONSERVER } from "$env/static/private";
	import ToDoHeader from "../toDoHeader.svelte";
    let toDoTitle: string = "";

    function storeTitle(){
        
    }
</script>


<ToDoHeader name = "john"/>
<p>make a new toDo:</p>
<form>
    <input type="text" placeholder="toDo Name" bind:value={toDoTitle}>
    <button type="submit" id="newToDoSubmitButton" on:click|preventDefault={storeTitle}>submit</button>
</form>



