<script lang="ts">
	import { onMount } from 'svelte';
	import { createDropdownMenu, melt } from '@melt-ui/svelte';
	import { Sun, Moon, Monitor } from 'lucide-svelte';

	const {
		elements: { trigger, menu, item, arrow }
	} = createDropdownMenu();

	let theme = 'system';
	let prefersDarkScheme = false;

	onMount(() => {
		prefersDarkScheme = window.matchMedia('(prefers-color-scheme: dark)').matches;
		// init the theme from local storage if available
		const saved_theme = localStorage.getItem('theme');
		if (saved_theme) {
			theme = saved_theme;
		}
	});

	function changeTheme(value: 'dark' | 'light' | 'system') {
		if (value === 'system') {
			localStorage.removeItem('theme');
			if (prefersDarkScheme) {
				document.documentElement.setAttribute('data-theme', 'dark');
			} else {
				document.documentElement.setAttribute('data-theme', 'light');
			}
		} else if (value === 'dark' || value === 'light') {
			localStorage.setItem('theme', value);
			document.documentElement.setAttribute('data-theme', value);
		}
		theme = value;
	}
	const light = () => changeTheme('light');
	const dark = () => changeTheme('dark');
	const system = () => changeTheme('system');
</script>

<button class="trigger" use:melt={$trigger} aria-label="Select theme">
	{#if theme === 'light' || (theme === 'system' && !prefersDarkScheme)}
		<Sun />
	{:else if theme === 'dark' || (theme === 'system' && prefersDarkScheme)}
		<Moon />
	{/if}
</button>

<div class="menu" use:melt={$menu}>
	<div use:melt={$item} class="menu__item" class:higlight={theme === 'light'} on:m-click={light}>
		<Sun />light
	</div>
	<div use:melt={$item} class="menu__item" class:higlight={theme === 'dark'} on:m-click={dark}>
		<Moon />dark
	</div>
	<div use:melt={$item} class="menu__item" class:higlight={theme === 'system'} on:m-click={system}>
		<Monitor />system
	</div>
	<div use:melt={$arrow} />
</div>

<style>
	.menu {
		z-index: 10;
		background-color: var(--popup-bkg-color);
		border-radius: 8px;
		padding: 8px;
		filter: drop-shadow(5px 5px 5px rgba(0, 0, 0, 0.2));
	}
	.trigger {
		border-radius: 50%;
		height: 40px;
		width: 40px;
		padding: 8px;
		border: none;
		cursor: pointer;
		background-color: transparent;
		color: var(--text-color);
	}
	.trigger:hover {
		background-color: var(--primary-color);
		color: #fff;
		border: none;
	}
	.menu__item {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 0.6rem;
		padding: 8px 16px;
		background-color: var(--popup-bkg-color);
	}
	.menu__item.higlight {
		color: var(--primary-color);
		font-weight: 500;
	}
	.menu__item:hover, .menu__item:focus, .menu__item:focus-visible {
		background-color: var(--primary-color);
		color: #fff;
		border-radius: 8px;
		border-width: 0;
	}
</style>
