<script lang="ts">
    import '../app.css';

    let {children} = $props();
</script>

<main class="flex flex-col items-center justify-center h-screen">
    {@render children()}
</main>

