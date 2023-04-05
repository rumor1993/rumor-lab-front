<script>
    import { onMount } from 'svelte';

    export let imageUrl;

    let textarea;

    onMount(() => {
        textarea.select();
        document.execCommand('copy');
    });
</script>

<textarea bind:value={imageUrl} bind:this={textarea}></textarea>

