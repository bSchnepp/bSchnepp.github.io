<script context="module" lang="ts">
	export const prerender = true;
</script>

<svelte:head>
	<title>Articles</title>
</svelte:head>

<div>
	<h1>Articles</h1>
	<section>
		<h2>AArch64 OS Development</h2>
			<h3><a href="/articles/arm/mmu">MMU Programming</a></h3>
			<h3><a href="/articles/arm/gic">GIC Programming</a></h3>
	</section>

	<section>
		<h2>Graphics Programming with OpenGL</h2>
			<h3>Nothing here yet!</h3>
	</section>
</div>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}

	h2 {
		font-size: 1.5em;
	}
	
	h3 {
		color: #cccccc;
	}
</style>
