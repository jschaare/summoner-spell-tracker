<script lang="ts">
    import Cooldown from "./cooldown.svelte";
    import { SummonerSpellData } from "../lib/summoner-spell-data";

    export let name;
    let sumSpell = SummonerSpellData.find((ss) => ss.name == name);
    console.log(sumSpell);

    let cdChild;
    let bgColor;
    let lucidityBoots = false;
    let cosmicInsight = false;

    $: timer = sumSpell.cooldown;
    $: iconUrl = sumSpell.icon_url;
    $: haste = (lucidityBoots ? 12 : 0) + (cosmicInsight ? 18 : 0);

    function setGreenBG() {
        bgColor = "bg-green-700";
    }

    function setRedBG() {
        bgColor = "bg-red-700";
    }
</script>

<div class="flex items-center max-w-xs {bgColor}">
    <img
        src={iconUrl}
        alt="Flash"
        on:click={() => cdChild.handleReset(haste)}
    />

    <div class="mx-auto p-4" on:click={() => cdChild.handleEnd()}>
        <div
            class="text-xl text-white font-semibold tracking-tight stroke-black"
        >
            <Cooldown
                countdown={timer}
                bind:this={cdChild}
                on:start={setGreenBG}
                on:end={setRedBG}
            />
        </div>
    </div>
    <div class="flex justify-center">
        <div>
            <div class="form-check">
                <input
                    class="form-check-input appearance-none h-4 w-4 border border-gray-300 rounded-sm bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 mt-1 align-top bg-no-repeat bg-center bg-contain float-left mr-2 cursor-pointer"
                    type="checkbox"
                    bind:checked={lucidityBoots}
                />
                <img
                    class="inline-block rounded-lg w-3/12"
                    src="https://ddragon.leagueoflegends.com/cdn/12.8.1/img/item/3158.png"
                    alt="lucidity boots"
                />
            </div>
            <div class="form-check ">
                <input
                    class="form-check-input appearance-none h-4 w-4 border border-gray-300 rounded-sm bg-white checked:bg-blue-600 checked:border-blue-600 focus:outline-none transition duration-200 mt-1 align-top bg-no-repeat bg-center bg-contain float-left mr-2 cursor-pointer"
                    type="checkbox"
                    bind:checked={cosmicInsight}
                />
                <img
                    class="inline-block rounded-lg w-3/12"
                    src="https://ddragon.leagueoflegends.com/cdn/img/perk-images/Styles/Inspiration/CosmicInsight/CosmicInsight.png"
                    alt="lucidity boots"
                />
            </div>
        </div>
    </div>
</div>
