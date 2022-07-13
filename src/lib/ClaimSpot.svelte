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
	const contractAddr = '0xB6aC9165d7c9752E7C7D09b5282FBdb5EfE6e308';
</script>

{#if !web3Props.account}
	<WalletConnect bind:web3Props {contractAddr} {contractAbi} />
{:else}
	<ClaimButton {web3Props} {contractAddr} {contractAbi} />
{/if}
