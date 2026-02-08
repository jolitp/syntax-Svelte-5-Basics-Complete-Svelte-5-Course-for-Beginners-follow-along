<script lang="ts">
	import { fromStore } from 'svelte/store';
    import Header from './Header.svelte'
    
    let form_state = $state({
        answers: {},
        step: 0,
        error: ''
    })
    
    const QUESTONS = [
        {
            question: "What is your name?",
            id: "name",
            type: "text",
        },
        {
            question: "What is your birthday?",
            id: "birthday",
            type: "date",
        },
        {
            question: "What is your favorite color?",
            id: "color",
            type: "color",
        },
    ]
    
    function nextStep(id: string) {
        if(!form_state.answers[id]) {
            form_state.step += 1;
            form_state.error = "";
        } else {
            form_state.error = "please fill out the form input"
        }
    }
</script>

<main>
    <Header name={form_state.answers.name}/>

    <p>step: {form_state.step + 1}</p>
    
    <!-- {#each QUESTONS as question (question.id)} -->
    {#each QUESTONS as { id, question, type }, index (id)}
        {#if form_state.step === index}
            {@render formStep({ question, id, type })}
        {/if}
    {/each}

    
    {#if form_state.error !== ""}
        <div>
            <p class="error">{form_state.error}</p>
        </div>
    {/if}
</main>

{JSON.stringify(form_state)}

{#snippet formStep({ question, id, type}: {
    type: string;
    id: string;
    question: string;
})}
    <article>
        <div>
            <label for={id}>{question}</label>
            <input {type} {id} bind:value={form_state.answers[id]}>
        </div>
        
        <button onclick={() => nextStep()}>Next</button>
    </article>
    
{/snippet}

<style>
    .error {
        color: darkred    }
</style>