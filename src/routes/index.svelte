<script>
    import Auth from '../components/Auth.svelte';
</script>

<h1 class="w3-jumbo w3-center">Glass</h1>
<p class="w3-large w3-center">Please log in</p>

<Auth on:auth={() => (window.location.href = '/group')} />
