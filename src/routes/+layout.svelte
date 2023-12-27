<script lang="ts">
	import '../app.css';
	import ThemeSwitcher from '$lib/ThemeSwitcher.svelte';
	
	
</script>

<nav class="app-bar">
	<ul>
		<li>
			<a href="/">Home</a>
		</li>
		<li>
			<a href="/about">About</a>
		</li>
		<li>
			<ThemeSwitcher />
		</li>
	</ul>
</nav>	
	
<main class="content">
	<slot />
</main>

<style>
	.app-bar ul {
		margin: 0;
		list-style-type: none;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		padding: 0 16px;
		height: 48px;
		gap: 1.5rem;
		background-color: var(--app-bar-bkg-color);
	}
	.app-bar ul li a {
		text-decoration: underline;
		color: var(--text-color);
	}
	.content {
		padding: 1rem;
		max-width: 36rem;
		margin: 0 auto;
	}
</style>
