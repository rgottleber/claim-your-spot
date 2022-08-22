<script>
	import { ethers } from 'ethers';
	import SPOTSAbi from '../contracts/SPOTS.json';
	// const contractAddr = '0xB6aC9165d7c9752E7C7D09b5282FBdb5EfE6e308';
	// const contractAddr = '0x138eA4251835a9166B9538cC22F25C34A155C531';
	const contractAddr = '0xFD346e90644cbDc8a74Ea7E300cb32c6c7e4668D';
	$: image = '';
	const url = 'https://goerli.infura.io/v3/9aa3d95b3bc440fa88ea12eaa4456161';
	var provider = new ethers.providers.JsonRpcProvider(url);
	// const provider = new ethers.providers.AlchemyProvider('rinkeby', apiKey);
	const contract = new ethers.Contract(contractAddr, SPOTSAbi.abi, provider);
	async function getSVG() {
		image = await contract.getSVG();
		console.log(image);
	}
	async function ethListen() {
		contract.on('SpotClaimed', async () => {
			getSVG();
		});
	}
	ethListen();
	getSVG();
</script>

<div class="w-5/6">
	<img src={image} alt="The NFT" class="w-auto h-auto" />
</div>
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
