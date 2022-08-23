<script>
	import { ethers } from 'ethers';
	import SPOTSAbi from '../contracts/SPOTS.json';
	// const contractAddr = '0xB6aC9165d7c9752E7C7D09b5282FBdb5EfE6e308';
	// const contractAddr = '0x138eA4251835a9166B9538cC22F25C34A155C531';
	// const contractAddr = '0xFD346e90644cbDc8a74Ea7E300cb32c6c7e4668D';
	const contractAddr = '0x3E8Bb76dc3aB7D86CEF28C0B0927AD16FC4EfD45';
	$: image = '';
	// const url = 'https://goerli.infura.io/v3/9aa3d95b3bc440fa88ea12eaa4456161';
	const url = 'https://api.avax-test.network/ext/bc/C/rpc';
	var provider = new ethers.providers.JsonRpcProvider(url);
	// const provider = new ethers.providers.AlchemyProvider('rinkeby', apiKey);
	const contract = new ethers.Contract(contractAddr, SPOTSAbi.abi, provider);
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
</script>

<img src={image} alt="The NFT" class="w-full h-auto shadow-primary border-accent border-2" />

<style>
	img {
		box-shadow: 7px 7px #00ff99;
	}
</style>
