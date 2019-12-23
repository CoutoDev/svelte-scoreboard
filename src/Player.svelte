<script>
import {
        createEventDispatcher
    } from "svelte";

    const dispatch = createEventDispatcher();

	export let name;
	export let points;
	let showControls = false;

	const addPoint = () => (points += 1);
	const removePoint = () => (points -= 1);
    const toggleControls = () => (showControls = !showControls);
    
    const onDelete = ()=>dispatch("removeplayer", name);
</script>

<main>
    <div class="card">
        <h1>
            {name}
            <button class="btn btn-sm" on:click={toggleControls}>
                {#if showControls}-{:else}+{/if}
            </button>
            <button class="btn btn-danger btn-sm"  on:click={onDelete}>X</button>
        </h1>
        <h3>Points: {points}</h3>
        {#if showControls}
            <button class="btn" on:click={addPoint}>+1</button>
            <button class="btn btn-dark" on:click={removePoint}>-1</button>
            <input type="number" bind:value={points}>
        {/if}
    </div>
</main>

<style>
	main {
		max-width: 100%;
	}

	h1 {
		color: #204f6e;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	h3{
		margin-bottom: 10px;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>