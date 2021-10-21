<script>
	import Navbar from '../components/Navbar.svelte';
</script>

<Navbar />

<main>
	<slot />
</main>

<footer>
	<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to learn SvelteKit</p>
</footer>

<style>
	/* @tailwind base; */
	/* @tailwind components; */
	/* @tailwind utilities; */
</style>
