<script>
	import { fly } from 'svelte/transition';

	export let tileIndex;
	export let num;

	let textTile;
	$: classTile = updateTile(num);

	function updateTile(numReceived) {
		textTile = '';
		if (numReceived > 0) {
			textTile = numReceived.toString();
			if (numReceived <= 4096) {
				return 'x' + numReceived.toString();
			} else {
				return 'x8192';
			}
		}
	}
</script>

<div id={tileIndex} class="tile {classTile}">
	{#key textTile}
		<span
			style="display: inline-block"
			in:fly={{ y: -20, duration: 1000 }}
			out:fly={{ y: 20, duration: 1000 }}
		>
			{textTile}
		</span>
	{/key}
</div>

<style>
	.tile {
		width: 90px;
		height: 90px;
		border: 5px solid #bbada0;

		font-size: 40px;
		font-weight: bold;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	/* colored tiles */

	.x2 {
		background-color: #eee4da;
		color: #727371;
	}

	.x4 {
		background-color: #ece0ca;
		color: #727371;
	}

	.x8 {
		background-color: #f4b17a;
		color: white;
	}

	.x16 {
		background-color: #f59575;
		color: white;
	}

	.x32 {
		background-color: #f57c5f;
		color: white;
	}

	.x64 {
		background-color: #f65d3b;
		color: white;
	}

	.x128 {
		background-color: #edce71;
		color: white;
	}

	.x256 {
		background-color: #edcc63;
		color: white;
	}

	.x512 {
		background-color: #edc651;
		color: white;
	}

	.x1024 {
		background-color: #eec744;
		color: white;
	}

	.x2048 {
		background-color: #ecc230;
		color: white;
	}

	.x4096 {
		background-color: #fe3d3d;
		color: white;
	}

	.x8192 {
		background-color: #ff2020;
		color: white;
	}
</style>
