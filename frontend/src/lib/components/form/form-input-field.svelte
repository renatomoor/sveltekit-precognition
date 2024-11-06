<script lang="ts">
    import type {HTMLInputAttributes} from "svelte/elements";
    import {Input, type InputEvents} from "$lib/components/ui/input";
    import {Label} from "$lib/components/ui/label";
    import {fade} from 'svelte/transition';

    type $$Props = HTMLInputAttributes & {
        class?: string;
        value?: string;
        label?: string;
        error?: string;
        readonly?: boolean;
    };
    
    type $$Events = InputEvents;

    let className: $$Props["class"] = undefined;
    export let value: $$Props["value"] = undefined;
    export let label: string = "";
    export let error: string = "";
    export {className as class};

    // Workaround for https://github.com/sveltejs/svelte/issues/9305
    // Fixed in Svelte 5, but not backported to 4.x.
    export let readonly: $$Props["readonly"] = undefined;
</script>

<div class="grid gap-2">
    {#if (label)}
        <Label>
            {label}
        </Label>
    {/if}

    <Input
        {...$$restProps}
        bind:value
        class="{error ? 'border-destructive' : ''} {className} transition duration-200 ease-in-out"
        on:blur
        on:change
        on:click
        on:focus
        on:focusin
        on:focusout
        on:input
        on:keydown
        on:keypress
        on:keyup
        on:mouseenter
        on:mouseleave
        on:mousemove
        on:mouseover
        on:paste
        {readonly}
    />

    {#if error}
        <p in:fade out:fade class="text-xs text-destructive">
            {error}
        </p>
    {/if}
</div>
