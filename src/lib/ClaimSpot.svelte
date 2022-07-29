<script>
	import { ethers } from 'ethers';

	import WalletConnect from '$lib/WalletConnect.svelte';
	import ClaimButton from '$lib/ClaimButton.svelte';
	import contractAbi from '../contracts/SPOTS.json';
	export let web3Props = {
		provider: null,
		signer: null,
		account: null,
		chainId: null,
		contract: null
	};
	const contractAddr = '0x138eA4251835a9166B9538cC22F25C34A155C531';
	async function switchChain() {
		try {
			// attempt to switch to Harmony One network
			const result = await ethereum.send('wallet_switchEthereumChain', [{ chainId: `0xa869` }]);
		} catch (switchError) {
			// 4902 indicates that the client does not recognize the Harmony One network
			if (switchError.code === 4902) {
				await ethereum.request({
					method: 'wallet_addEthereumChain',
					params: [
						{
							chainId: '0xa869',
							rpcUrls: [
								'https://api.avax-test.network/ext/bc/C/rpc',
								'https://rpc.ankr.com/avalanche_fuji'
							],
							chainName: 'Avalanche Fuji Testnet',
							nativeCurrency: { name: 'AVAX', decimals: 18, symbol: 'AVAX' },
							blockExplorerUrls: ['https://testnet.snowtrace.io']
						}
					]
				});
			}
		}
		window.location.reload();
	}
</script>

{#if !web3Props.account}
	<WalletConnect bind:web3Props {contractAddr} {contractAbi} />
{:else if web3Props.chainId === 43113}
	<ClaimButton {web3Props} {contractAddr} {contractAbi} />
{:else}
	<div class="grid h-screen place-items-center">
		<div class="text-center">
			<h1 class="text-4xl">You are not on the Fuji network.</h1>
			<p class="text-lg">Please switch to the Fuji network to claim your spot.</p>
			<button class="btn" on:click={switchChain}>Switch to Fuji</button>
		</div>
	</div>
{/if}
