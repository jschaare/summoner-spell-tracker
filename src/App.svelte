<script lang="ts">
	import "./tailwind.svelte";
	import Summoner from "./components/summoner.svelte";
</script>

<main>
	<Summoner position={"TOP"} />
	<Summoner position={"JUNGLE"} />
	<Summoner position={"MID"} />
	<Summoner position={"ADC"} />
	<Summoner position={"SUPPORT"} />
</main>

<style>
</style>
