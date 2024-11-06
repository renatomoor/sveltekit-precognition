<script lang="ts">
    import {fade} from 'svelte/transition';

    interface Props {
        children?: import('svelte').Snippet;
        error?: string;
        success?: string;

        [key: string]: any
    }

    let {children, error, success, ...rest}: Props = $props();

</script>

<form {...rest}>
    {#if error}
        <div in:fade out:fade class="text-red-500 text-sm">{error}</div>
    {/if}

    {#if success}
        <div in:fade out:fade class="text-green-500 text-sm">{success}</div>
    {/if}


    {@render children?.()}
</form>
