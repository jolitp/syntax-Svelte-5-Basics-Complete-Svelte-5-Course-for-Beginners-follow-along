<script lang="ts">
	import { fromStore } from 'svelte/store';
    import Header from './Header.svelte'
    
    let form_state = $state({
        name: "",
        birthday: "",
        step: 0,
        error: ''
    })
</script>

<main>
    <Header name={form_state.name}>
        <p>hello</p>
        {#snippet second_child(name)}
            <p>second child {name}</p> 
        {/snippet}
    </Header>

    <p>step: {form_state.step + 1}</p>
    
    {@render formStep({
        question: "Wheat's your name",
        id: "name",
        type: "text"
    })}

    
    {#if form_state.error !== ""}
        <div>
            <p class="error">{form_state.error}</p>
        </div>
    {/if}
</main>

{#snippet formStep({ question, id, type}: {
    type: string;
    id: string;
    question: string;
})}
    <article>
        <div>
            <label for={id}>{question}</label>
            <input {type} {id} bind:value={form_state[id]}>
        </div>
    </article>
    
{/snippet}

<style>
    .error {
        color: darkred    }
</style>