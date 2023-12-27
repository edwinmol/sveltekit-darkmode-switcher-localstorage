<script lang="ts">
	import '../app.css';
	import ThemeSwitcher from '$lib/ThemeSwitcher.svelte';
	
	
</script>

<div class="app-bar">
	<ThemeSwitcher />
</div>
<main class="content">
	<slot />
</main>

<style>
	.app-bar {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		padding: 0 16px;
		height: 48px;
		background-color: var(--app-bar-bkg-color);
	}
	.content {
		padding: 1rem;
		max-width: 36rem;
		margin: 0 auto;
	}
	/* TODO: set the font family and use a variable 
    font: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_fonts/Variable_fonts_guide */
</style>
