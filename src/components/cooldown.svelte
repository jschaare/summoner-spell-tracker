<script lang="ts">
	import { createEventDispatcher, onMount } from "svelte";
	import CooldownTime from "./cooldown-time.svelte";

	const dispatch = createEventDispatcher();

	export let countdown;

	let now = Date.now();
	let end = now + countdown * 1000;

	$: count = Math.round((end - now) / 1000);
	$: h = Math.floor(count / 3600);
	$: m = Math.floor((count - h * 3600) / 60);
	$: s = count - h * 3600 - m * 60;

	function updateTimer() {
		now = Date.now();
	}

	let interval = setInterval(updateTimer, 1000);
	$: if (count === 0) handleEnd();

	export function handleReset(haste) {
		clearInterval(interval);
		now = Date.now();
		let cd = (countdown * 100) / (100 + haste);
		end = now + cd * 1000;
		interval = setInterval(updateTimer, 1000);
		dispatch("start");
	}

	export function handleEnd() {
		count = 0;
		clearInterval(interval);
		dispatch("end");
	}

	onMount(async () => {
		count = 0;
	});
</script>

<div>
	{#if count > 0}
		<CooldownTime minutes={m} seconds={s} />
	{:else}
		Available!
	{/if}
</div>
