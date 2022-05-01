<script>
	import { getContext } from 'svelte';
	export let message;
	export let hasForm = false;
	export let onCancel = (value = null) => {};
	export let onOkay = (value = null) => {};

	const { close } = getContext('simple-modal');

	let value;

	function _onCancel() {
		onCancel();
		close();
	}

	function _onOkay() {
		onOkay(value);
		close();
	}
</script>

<h2>{message}</h2>

{#if hasForm}
	<input type="text" bind:value on:keydown={(e) => e.which === 13 && _onOkay()} />
{/if}

<div class="buttons">
	<button on:click={_onCancel}> Non </button>
	<button on:click={_onOkay}> Oui </button>
</div>

<style>
	h2 {
		font-size: 2rem;
		text-align: center;
	}

	input {
		width: 100%;
	}

	.buttons {
		display: flex;
		justify-content: space-evenly;
	}
</style>
