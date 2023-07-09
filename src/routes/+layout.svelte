<script>
	import '../app.postcss';
	import './styles.css';
	import Navbar from './Navbar.svelte';
	import Footer from './Footer.svelte';
</script>

<div class="app">
	<header class="relative px-8 pb-10">
		<Navbar />
	</header>

	<main>
		<slot />
	</main>

	<footer class="pt-20">
		<Footer />
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>
