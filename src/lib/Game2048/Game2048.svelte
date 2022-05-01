<script>
	import Tile from './components/Tile.svelte';
	import { onMount } from 'svelte';
	import { getContext } from 'svelte';
	import Popup from '../common/Popup.svelte';
	const { open } = getContext('simple-modal');

	let board = [];
	let score;
	let rows = 4;
	let columns = 4;
	let gameOver = false;

	const ARROWS_KEYS = ['ArrowDown', 'ArrowUp', 'ArrowLeft', 'ArrowRight'];

	onMount(() => {
		setGame();
	});

	function setGame() {
		score = 0;
		board = [
			[0, 0, 0, 0],
			[0, 0, 0, 0],
			[0, 0, 0, 0],
			[0, 0, 0, 0]
		];

		//create 2 to begin the game
		setTwo();
		setTwo();
	}

	function setTwo() {
		if (!hasEmptyTile()) {
			return;
		}
		let found = false;
		while (!found) {
			//find random row and column to place a 2 in
			let r = Math.floor(Math.random() * rows);
			let c = Math.floor(Math.random() * columns);
			if (board[r][c] == 0) {
				board[r][c] = 2;
				found = true;
			}
		}
		if (!hasPossibleMove()) {
			console.log('after setTwo gameOver', board);
			setGameOver();
		}
	}

	function setGameOver() {
		gameOver = true;
		showDialog();
	}

	function hasEmptyTile() {
		for (let r = 0; r < rows; r++) {
			for (let c = 0; c < columns; c++) {
				if (board[r][c] == 0) {
					//at least one zero in the board
					return true;
				}
			}
		}

		return false;
	}

	function testPossibleMoveOfRow(row) {
		for (let c = 0; c < columns - 1; c++) {
			if (row[c] == row[c + 1] || row[c + 1] == 0 || row[c] == 0) {
				return true;
			}
		}

		return false;
	}

	function hasPossibleMove() {
		for (let r = 0; r < rows; r++) {
			if (testPossibleMoveOfRow(board[r])) {
				return true;
			}
		}

		for (let c = 0; c < columns; c++) {
			let rowBuilded = [];
			for (let r = 0; r < rows; r++) {
				rowBuilded.push(board[r][c]);
			}
			if (testPossibleMoveOfRow(rowBuilded)) {
				return true;
			}
		}

		return false;
	}

	function handleKeydown(event) {
		const keyPush = event.key;
		if (!gameOver && ARROWS_KEYS.includes(keyPush)) {
			switch (keyPush) {
				case 'ArrowLeft':
					slideLeft();
					break;
				case 'ArrowRight':
					slideRight();
					break;
				case 'ArrowUp':
					slideUp();
					break;
				case 'ArrowDown':
					slideDown();
					break;
				default:
			}

			if (!gameOver) {
				setTwo();
			}
		}
	}

	function filterZero(row) {
		return row.filter((num) => num != 0); //create new array of all nums != 0
	}

	function slide(row) {
		//[0, 2, 2, 2]
		row = filterZero(row); //[2, 2, 2]
		for (let i = 0; i < row.length - 1; i++) {
			if (row[i] == row[i + 1]) {
				row[i] *= 2;
				row[i + 1] = 0;
				score += row[i];
			}
		} //[4, 0, 2]
		row = filterZero(row); //[4, 2]
		//add zeroes
		while (row.length < columns) {
			row.push(0);
		} //[4, 2, 0, 0]
		return row;
	}

	function slideLeft() {
		for (let r = 0; r < rows; r++) {
			let row = board[r];
			row = slide(row);
			board[r] = row;
		}
		checkGameOver();
	}

	function slideRight() {
		for (let r = 0; r < rows; r++) {
			let row = board[r]; //[0, 2, 2, 2]
			row.reverse(); //[2, 2, 2, 0]
			row = slide(row); //[4, 2, 0, 0]
			board[r] = row.reverse(); //[0, 0, 2, 4];
		}
		checkGameOver();
	}

	function slideUp() {
		for (let c = 0; c < columns; c++) {
			let rowBuilded = [];
			for (let r = 0; r < rows; r++) {
				rowBuilded.push(board[r][c]);
			}
			let row = rowBuilded;
			row = slide(row);
			// board[0][c] = row[0];
			// board[1][c] = row[1];
			// board[2][c] = row[2];
			// board[3][c] = row[3];
			for (let r = 0; r < rows; r++) {
				board[r][c] = row[r];
			}
		}
		checkGameOver();
	}

	function slideDown() {
		for (let c = 0; c < columns; c++) {
			let row = [];
			for (let r = 0; r < rows; r++) {
				row.push(board[r][c]);
			}
			row.reverse();
			row = slide(row);
			row.reverse();
			for (let r = 0; r < rows; r++) {
				board[r][c] = row[r];
			}
		}
		checkGameOver();
	}

	function checkGameOver() {
		if (!hasPossibleMove()) {
			setGameOver();
		}
	}

	const onCancel = (value) => {};

	const onOkay = (text) => {
		gameOver = false;
		setGame();
	};

	const showDialog = () => {
		open(
			Popup,
			{
				message: 'Recommencer un 2048?',
				hasForm: false,
				onCancel,
				onOkay
			},
			{
				closeButton: false,
				closeOnEsc: false,
				closeOnOuterClick: false
			}
		);
	};
</script>

<svelte:window on:keydown={handleKeydown} />

<h1>2048</h1>
<hr />

<h2>Score: <span id="score">{score}</span></h2>

<div id="board">
	{#each board as row, r}
		{#each row as _, c}
			<Tile tileIndex={r.toString() + '-' + c.toString()} num={board[r][c]} />
		{/each}
	{/each}
</div>

<button on:click={setGameOver}> Recommencer </button>

<style>
	hr {
		width: 500px;
	}

	h1 {
		margin: 0;
	}

	h2 {
		font-size: 1.5em;
		margin-block-start: 0.83em;
		margin-block-end: 0.83em;
		margin-inline-start: 0px;
		margin-inline-end: 0px;
		font-weight: bold;
	}

	#board {
		width: 400px;
		height: 400px;

		background-color: #cdc1b5;
		border: 6px solid #bbada0;

		margin: 0 auto;
		display: flex;
		flex-wrap: wrap;
	}
</style>
