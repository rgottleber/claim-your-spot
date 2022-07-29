<script>
	import { ethers } from 'ethers';
	import { onMount } from 'svelte';

	// const apiKey = import.meta.env.VITE_RINKEBY_API_KEY;
	const colors = ['#3F5ACB', '#EA5D65', '#F0CD49', '#FFFFFF'];
	import SPOTSAbi from '../contracts/SPOTS.json';
	export let width;
	export let height;
	// const contractAddr = '0xB6aC9165d7c9752E7C7D09b5282FBdb5EfE6e308';
	const contractAddr = '0x138eA4251835a9166B9538cC22F25C34A155C531';
	$: image = '';
	const url = 'https://api.avax-test.network/ext/bc/C/rpc';
	var provider = new ethers.providers.JsonRpcProvider(url);
	// const provider = new ethers.providers.AlchemyProvider('rinkeby', apiKey);
	const contract = new ethers.Contract(contractAddr, SPOTSAbi.abi, provider);
	onMount(async () => {
		async function getSVG() {
			image = await contract.getSVG();
		}
		async function ethListen() {
			contract.on('SpotClaimed', async () => {
				getSVG();
			});
		}
		ethListen();
		getSVG();
	});
</script>

<svelte:window bind:innerWidth={width} bind:innerHeight={height} />
{@html image}

<!-- <svg viewBox="0 0 {width} {height}" preserveAspectRatio="xMidYMid meet">
	<rect {width} {height} fill="#1A1B27" />
	{#each points as point, i}
		{#if i == points.length - 1}
			<circle cx={point.x} cy={point.y} class="pulse" r={point.r} fill={point.fill} />
		{:else}
			<circle cx={point.x} cy={point.y} r={point.r} fill={point.fill} />
		{/if}
		/>
	{/each}
</svg> -->
