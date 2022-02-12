<script lang="ts">
	import { page } from '$app/stores';
	import feather from 'feather-icons';
</script>

<header>
	<nav>
		<ul>
			<li class:active={$page.url.pathname === '/'}><a sveltekit:prefetch href="/">Home</a></li>
			<li class:active={$page.url.pathname === '/projects'}>
				<a sveltekit:prefetch href="/projects">Projects</a>
			</li>
			<li class:active={$page.url.pathname === '/articles'}>
				<a sveltekit:prefetch href="/articles">Articles</a>
			</li>
		</ul>
		<svg viewBox="0 0 4 3" aria-hidden="true">
			<path d="M0,0 L0,3 C0,3 2,3 3,2 L3,0 Z" />
		</svg>			
	</nav>
	<div>
		<a class="vertli" href="https://github.com/bSchnepp">{@html feather.icons.github.toSvg()}</a>
		<a class="vertli" href="https://twitter.com/brschnepp">{@html feather.icons.twitter.toSvg()}</a>
	</div>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
		position: fixed;
		top: 0;
		width: 100%;
	}

	.vertli {
		display: block;
		text-align: center;
		margin-left: 2em;
	}

	nav {
		display: flex;
		justify-content: center;
		--background: rgba(235, 235, 235, 0.9);
	}

	svg {
		width: 4em;
		height: 3em;
		display: block;
	}

	path {
		fill: var(--background);
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
	}

	li.active::before {
		--size: 6px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--accent-color);
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 1em;
		color: var(--heading-color);
		font-weight: 700;
		font-size: 0.95rem;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--accent-color);
	}
</style>
