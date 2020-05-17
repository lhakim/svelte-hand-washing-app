<script>
    import Timer from './Timer.svelte';
    import HowTo from './HowTo.svelte';
    let audio;

    function timerEnds() {
        audio.play();
    }
</script>
<style>
    h1 {
        text-align: center
    }
</style>
<h1>Hand Washing App</h1>

<Timer on:end={timerEnds} />

<HowTo />

<audio bind:this={audio}>
    <source src="sound.wav" />
</audio>