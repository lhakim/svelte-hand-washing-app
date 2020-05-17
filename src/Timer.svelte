<script>
    import { createEventDispatcher } from "svelte";
    import ProgressBar from './ProgressBar.svelte';
    const totalSeconds = 20;
    let secondLeft = totalSeconds;
    let percentageCompleted = 0;
    let isRunning = false;
    $: progress = ((totalSeconds - secondLeft)/totalSeconds) * 100;

    const dispatch = createEventDispatcher();
    function startTimer(){
        isRunning = true;
        const timer = setInterval(() => {
            secondLeft -= 1;
            if(secondLeft == 0) {
                clearInterval(timer);
                secondLeft = totalSeconds;
                isRunning = false;
                dispatch('end');
            }
        }, 1000);
    }
</script>

<style>
    h2 {
        margin: 0;
    }

    .start {
        background-color: rgba(154, 70, 70);
        width: 100%;
        margin: 10px 0;
        color: white;
    }
    .start[disabled] {
        background-color: rgb(194, 194, 194);
        cursor: not-allowed;
    }
</style>
<div bp="grid">
    <h2 bp="offset-5@md 4@md 12@sm">Seconds Left:{secondLeft}</h2>
</div>

<ProgressBar {progress} />

<div bp="grid">
    <button disabled={isRunning} on:click={startTimer} bp="offset-5@md 4@md 12@sm" class="start">Start</button>
</div>
