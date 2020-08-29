<script>
	import Face from "./Face.svelte";
	import Container from "./Container.svelte";
	import Header from "./Header.svelte";
	import Buttons from "./Button.svelte";

	import store from "./store";

	let header = false;
	let happyScore = 0;
	let storeIndex = 0;
	let name = '';

	$: smileySays = store[storeIndex].smileySays;
	$: if (!smileySays) {
		const end = store[storeIndex].end;
		if (happyScore < 0) {
			smileySays = end.mean;
		} else if (happyScore === 0) {
			smileySays = end.neutral;
		} else {
			smileySays = end.nice;
		}

		if (name.length > 0) {
			smileySays = name + ', ' + smileySays;
		}
	}
	$: buttons = store[storeIndex].buttons;

	function clickHandler(e) {

		if (e.detail.value === 'reset') {
			storeIndex = 0;
			happyScore = 0;
			header = false;
			return;
		}

		happyScore += e.detail.value;

		if (e.detail.value == 2) {
			header = true;
		}

		storeIndex = storeIndex + 1;
	}
</script>

{#if header}
	<Header />
{/if}

<Container>
	<input type="text" bind:value={name} />
	<h1>{smileySays}</h1>
	<Face {happyScore} size={3} />
	<Buttons {buttons} on:click={clickHandler} />
</Container>

<!-- Final Challenge
2. Display final message depending on happyScore
3. Implement the Reset functionality
-->


<style>
	div {
		color: red;
	}
	:global(*) {
		box-sizing: border-box;
	}
	:global(body, html) {
		margin: 0;
		padding: 0;
		height: 100vh;
		overflow: hidden;
	}

	h1 {
		text-align: center;
		background: #ff3e00;
		font-size: 2em;
		padding: 0.3em 0.6em;
		color: white;
		border-radius: 50px;
	}

	input {
		margin: 1em;
		width: 250px;
		border: 0;
		outline: 0;
		background: transparent;
		border-bottom: 1px solid black;
		text-align: center;
		font-size: 2em;
	}
</style>