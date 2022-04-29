<script lang="ts">
	import SummonerSpellTimer from "./summoner-spell-timer.svelte";
	import { SummonerSpellData } from "../lib/summoner-spell-data";

	export let position;

	let selected0;
	let selected1;
	let isSelected = false;

	function handleSubmit() {
		isSelected = true;
	}
	function handleReset() {
		isSelected = false;
	}
</script>

<div class="outline outline-gray-800 bg-gray-800">
	<h1
		class="text-white flex justify-center font-semibold"
		on:click={handleReset}
	>
		{position}
	</h1>
	{#if isSelected}
		<SummonerSpellTimer name={selected0.name} />
		<SummonerSpellTimer name={selected1.name} />
	{:else}
		<form
			on:submit|preventDefault={handleSubmit}
			class="flex justify-around"
		>
			<div class="dropdown inline-block relative">
				<select
					bind:value={selected0}
					class="bg-gray-500 text-white rounded inline-flex items-center capitalize"
				>
					{#each SummonerSpellData as spell}
						<option value={spell} class="capitalize">
							{spell.name}
						</option>
					{/each}
				</select>
			</div>
			<div class="dropdown inline-block relative">
				<select
					bind:value={selected1}
					class="bg-gray-500 text-white rounded inline-flex items-center capitalize"
				>
					{#each SummonerSpellData as spell}
						<option value={spell} class="capitalize">
							{spell.name}
						</option>
					{/each}
				</select>
			</div>
			<button
				type="submit"
				class="inline-block rounded-md bg-blue-600 border-blue-600 hover:bg-blue-700 hover:border-blue-700 text-white font-semibold"
			>
				Submit
			</button>
		</form>
	{/if}
</div>
