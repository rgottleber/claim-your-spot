<script>
	import { ethers } from 'ethers';
	export let web3Props = {
		provider: null,
		signer: null,
		account: null,
		chainId: null,
		contract: null
	};
	export let contractAbi;
	export let contractAddr;

	async function connectWallet() {
		let provider = new ethers.providers.Web3Provider(window.ethereum, 'any');
		await provider.send('eth_requestAccounts', []);
		const signer = provider.getSigner();
		const account = await signer.getAddress();
		const chainId = await signer.getChainId();
		const contract = new ethers.Contract(contractAddr, contractAbi.abi, signer);
		web3Props = { signer, provider, chainId, account, contract };
	}
</script>

{#if !web3Props.account}
	<div class="grid h-screen place-items-center">
		<button class="btn" on:click={connectWallet}>Attach Wallet</button>
	</div>
{/if}
