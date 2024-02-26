<script>
    import { onMount } from 'svelte';
    export let urlResult;

    let texarea;
    onMount(() => {
        texarea.select();
        document.execCommand('copy');
    });
</script>

<textarea bind:value={urlResult} bind:this={texarea} cols="30" rows="10"></textarea>