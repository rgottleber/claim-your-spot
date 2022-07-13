<script>
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
	const contractAddr = '0x68043cACEe43f8284D05a0C5D8663D5D44172367';
</script>

{#if !web3Props.account}
	<WalletConnect bind:web3Props {contractAddr} {contractAbi} />
{:else}
	<ClaimButton {web3Props} {contractAddr} {contractAbi} />
{/if}
