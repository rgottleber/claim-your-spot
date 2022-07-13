<script>
	// import { ethers } from 'ethers';
	import { onMount } from 'svelte';

	// const apiKey = import.meta.env.VITE_RINKEBY_API_KEY;
	const colors = ['#3F5ACB', '#EA5D65', '#F0CD49', '#FFFFFF'];
	// import NFTAbi from '../contracts/NFT.json';
	export let width;
	export let height;
	$: contractAddr = '';
	// $: values = [];
	$: points = [];
	async function getETHValues() {
		const provider = new ethers.providers.AlchemyProvider(chain, apiKey);

		const contract = new ethers.Contract(contractAddr, NFTAbi.abi, provider);
		values = await contract.getValues();
		console.log(values);
	}
	let values = [
		3333, 32261, 2975, 87407, 60248, 65644, 61903, 38974, 29201, 27728, 56651, 57720, 96304, 46102,
		80202, 1805, 53798, 23490, 67208, 84012, 58227, 17753, 23882, 12922, 89941, 6970, 48687, 40744,
		68906, 2297, 87791, 81209, 909, 14540, 90083, 96833, 54001, 21337, 34876, 27568, 95260
	];
	onMount(async () => {
		// let txn = await getETHValues();
		// txn.wait();
		values.forEach((val) => {
			points.push({ x: val % width, y: val % height, r: (val % 8) + 2, fill: colors[val % 4] });
		});
		points = points;
		console.log(points);
	});
</script>

<svelte:window bind:innerWidth={width} bind:innerHeight={height} />

<svg viewBox="0 0 {width} {height}" preserveAspectRatio="xMidYMid meet">
	<rect {width} {height} fill="#1A1B27" />
	{#each points as point, i}
		{#if i == points.length - 1}
			<circle
				cx={point.x}
				cy={point.y}
				r={point.r}
				class="pulse"
				fill={point.fill}
				stroke={point.fill}
			/>
		{:else}
			<circle cx={point.x} cy={point.y} r={point.r} fill={point.fill} />
		{/if}
		/>
	{/each}
</svg>

<style>
	svg {
		width: 100%;
	}
	.pulse {
		stroke-width: 50;
		animation: circle_animation 2s linear infinite;
	}
	@keyframes circle_animation {
		0% {
			stroke-width: 0;
		}
		50% {
			stroke-width: 50;
		}
		100% {
			stroke-width: 0;
		}
	}
</style>
