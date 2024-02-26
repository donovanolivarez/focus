<!-- stub for the timer component -->
<script lang="ts">
	// init a timer here.
	let seconds: number = 5;
	let minutes: number = 0;
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

	function startTimer() {
		timerInterval = setInterval(updateTimer, 1000);
	}

	function stopTimer() {
		clearInterval(timerInterval);
	}
	function increaseTime() {
		minutes += 5;
		clock = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
	}

	function decreaseTime() {
		minutes -= 5;
		clock = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
	}
</script>

<div class="timer">
	<h1 class="text-center font-bold text-4xl">Focus Timer</h1>
	<h2 class="text-center  text-8xl py-10">{clock}</h2>
<!--	Focus session is done, display message to the user. -->
	{#if minutes === 0 && seconds === 0}
		<p>Session complete!</p>
	{/if}
</div>

<div class="text-center">
	<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click={increaseTime}>+ 5 Minutes </button>
	<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click={decreaseTime}>- 5 Minutes</button>
	<button class="changeTimeButton" on:click={startTimer}>Start</button>
	<button class="changeTimeButton" on:click={stopTimer}>Stop</button>
</div>

<style>
    h1 {
        color: green;
    }
</style>