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
	<h1>Focus Timer</h1>
	<h2>{clock}</h2>
<!--	Focus session is done, display message to the user. -->
	{#if minutes === 0 && seconds === 0}
		<p>Session complete!</p>
	{/if}
</div>

<div class="timerControls">
	<button class="changeTimeButton" on:click={increaseTime}>+</button>
	<button class="changeTimeButton" on:click={decreaseTime}>-</button>
	<button class="changeTimeButton" on:click={startTimer}>Start</button>
	<button class="changeTimeButton" on:click={stopTimer}>Stop</button>
</div>

<style>
    h1 {
        color: green;
    }
</style>