<!-- stub for the timer component -->
<script lang="ts">
	// init a timer here.
	let seconds: number = 0;
	let minutes: number = 25;
	let clock: string = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
	let timerInterval: number = 0;

	function updateTimer() {
		if (minutes === 0 && seconds === 0) {
			clearInterval(timerInterval);
			return;
		}
		if (seconds % 60 === 0) {
			seconds = 60;
			minutes -= 1;
		}
		seconds -= 1;
		clock = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
	}

	// clicking this multiple times easily breaks the timer.
	function startTimer() {
		timerInterval = setInterval(updateTimer, 1000);
	}

	function pauseTimer() {
		clearInterval(timerInterval);
		timerInterval = 0;
	}
	function increaseTime() {
		minutes += 5;
		clock = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
	}

	function decreaseTime() {
		if (minutes > 0) {
			minutes -= 5;
		}

		// user set the time below zero, so reset back to zero.
		if (minutes < 0) {
			minutes = 0
		}
		clock = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
	}

	// fully reset the timer
	function resetTimer() {
		minutes = 25;
		seconds = 0;
		clock = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
		clearInterval(timerInterval);
		timerInterval = 0;
	}
</script>

<div class="timer">
	<h1 class="text-center font-bold text-4xl text-green-500">Focus Timer</h1>
	<h2 class="text-center  text-8xl py-10">{clock}</h2>
<!--	Focus session is done, display message to the user. -->
	{#if minutes === 0 && seconds === 0}
		<p class="text-center font-bold text-2xl text-green-500">Session complete!</p>
	{/if}
</div>

<div class="text-center">
	<button class=" hover:bg-gray-800 text-white font-bold py-2 px-4 rounded {timerInterval !== 0 ? 'cursor-not-allowed' : ''}" on:click={increaseTime}>+ 5 Minutes </button>
	<button class="hover:bg-gray-800 text-white font-bold py-2 px-4 rounded {timerInterval !== 0 ? 'cursor-not-allowed' : ''}" on:click={decreaseTime}>- 5 Minutes</button>
	<button class=" hover:bg-gray-800 text-white font-bold py-2 px-4 rounded {timerInterval !== 0 ? 'cursor-not-allowed' : ''}" on:click={startTimer} disabled={timerInterval !== 0}>Start</button>
	<button class=" hover:bg-gray-800 text-white font-bold py-2 px-4 rounded" on:click={pauseTimer}>Pause</button>
	<button class=" hover:bg-gray-800 text-white font-bold py-2 px-4 rounded" on:click={resetTimer}>Reset</button>
</div>