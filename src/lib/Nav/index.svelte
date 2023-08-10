<script>
	import { tabs } from '$lib/utils/tabs';
	import NavSmall from './NavSmall.svelte';
	import NavLarge from './NavLarge.svelte';
    import { page } from '$app/stores';	
	import IconButton from '@smui/icon-button';
	import { Icon } from '@smui/common';

	$: active = tabs.find(tab => tab.dest == $page.url.pathname || (tab.nest && tab.children.find(subTab => subTab.dest == $page.url.pathname)));
</script>

<svelte:head>
	<title>{!$page.url.pathname[1] ? 'Home' : $page.url.pathname[1].toUpperCase() + $page.url.pathname.slice(2)} | League Page</title>
</svelte:head>

<style>
	a {
		display: table;
    	margin: 0 auto;
	}
	nav {
		background-color: var(--fff);
		position: relative;
		z-index: 2;
		border-bottom: 1px solid #00316b;
	}

	#logo {
		display: block;
		margin: 0 auto;
	}

    .large {
		display: block;
    }

	.small {
		display: none;
	}

	.container {
		position: absolute;
		top: 0.25em;
		right: 0.25em;
	}

	:global(.lightDark) {
		color: var(--g555)
	}

	@media (max-width: 950px) { /* width of the large navBar */
		.large {
			display: none;
		}

		.small {
			display: block;
		}
	}
</style>

<nav>
	<a href="/"><img id="logo" alt="league logo" src="./badge.png" /></a>
	<div class="large">
		<NavLarge {tabs} bind:active={active} />
	</div>
	<div class="small">
		<NavSmall {tabs} bind:active={$page.url.pathname} />
	</div>

</nav>
