<script context="module">
	import Modal from 'svelte-simple-modal';
	import Game2048 from '../../lib/Game2048/Game2048.svelte';
	export const prerender = true;
</script>

<svelte:head>
	<title>Games</title>
</svelte:head>

<Modal>
	<section>
		<Game2048 />
	</section>
</Modal>

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

	.welcome {
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
