<script lang="ts">
	import type { Snippet } from "svelte";

    let { name, children, second_child }: {
        name: string;
        children: Snippet;
        second_child: Snippet;
        } = $props();
</script>

<div>
    <h1>
        {name ? name : "User"}'s Form
    </h1>
    
    {@render children()}
    
    <h3>{@render second_child('Scott')}</h3>
</div>
