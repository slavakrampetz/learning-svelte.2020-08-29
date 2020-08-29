<script>

import { each } from "svelte/internal";

const loops = [1];

</script>

<header>
	{#each loops as _}
		<img alt="svelte logo" src="./img/svelte-logo.svg">
		<span>;)</span>
	{/each}

</header>

<style>
	img {
		height: 100%;
	}

  header {
		position: absolute;
		height: 100px;
		width: 100%;
		color: white;
		font-size: 5em;
		overflow: hidden;
		display: flex;
		justify-content: space-between;
	}
</style>