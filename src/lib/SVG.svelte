<script>
	import { ethers } from 'ethers';
	import { onMount } from 'svelte';

	const apiKey = import.meta.env.VITE_RINKEBY_API_KEY;
	const colors = ['#3F5ACB', '#EA5D65', '#F0CD49', '#FFFFFF'];
	import SPOTSAbi from '../contracts/SPOTS.json';
	export let width;
	export let height;
	const contractAddr = '0xB6aC9165d7c9752E7C7D09b5282FBdb5EfE6e308';
	$: values = [];
	$: points = [];
	const provider = new ethers.providers.AlchemyProvider('rinkeby', apiKey);
	const contract = new ethers.Contract(contractAddr, SPOTSAbi.abi, provider);
	onMount(async () => {
		async function getETHValues() {
			values = await contract.getAllSpots();
			values.forEach((bigVal) => {
				points.push({
					x: bigVal.mod(width).toNumber(),
					y: bigVal.mod(height).toNumber(),
					r: bigVal.mod(8).toNumber() + 2,
					fill: colors[bigVal.mod(4).toNumber()]
				});
			});
			points = points;
			contract.on('SpotClaimed', async () => {
				getEthValues();
			});

			console.log('here', points);
			console.log(values);
		}
		async function ethListen() {
			contract.on('SpotClaimed', async () => {
				getETHValues();
			});
		}
		ethListen();
		getETHValues();
	});
</script>

<svelte:window bind:innerWidth={width} bind:innerHeight={height} />

<svg viewBox="0 0 {width} {height}" preserveAspectRatio="xMidYMid meet">
	<rect {width} {height} fill="#1A1B27" />
	{#each points as point, i}
		{#if i == points.length - 1}
			<circle cx={point.x} cy={point.y} class="pulse" r={point.r} fill={point.fill} />
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
		animation: circle_animation 3s linear infinite;
	}
	@keyframes circle_animation {
		0% {
		}
		50% {
			r: 50;
		}
		100% {
		}
	}
</style>
