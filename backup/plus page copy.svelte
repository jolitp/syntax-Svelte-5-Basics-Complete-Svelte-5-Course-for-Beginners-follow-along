<script lang="ts">
    import Header from '../src/routes/Header.svelte'
    let name = $state('Scott');
    let full_name = $derived(name + " " + 'Tolinski');
    
    let status: "OPEN" | "CLOSED" = $state("OPEN")
    
    function onclick() {
        status = status === "OPEN" ? "CLOSED" : "OPEN"
    }
</script>

<Header {name} fake_name="wes"/>

<h2>{full_name}</h2>

<input type="text" bind:value={name} />

<p>The store is now {status}</p>

<button {onclick}>Toggle Status</button>