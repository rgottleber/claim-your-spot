<script>
	$: claimed = false;
	$: waiting = false;
	export let web3Props = {
		provider: null,
		signer: null,
		account: null,
		chainId: null,
		contract: null
	};
	async function claimYourSpot() {
		let spotTXN = await web3Props.contract.claimYourSpot();
		waiting = true;
		spotTXN.wait();
		waiting = false;
		claimed = true;
	}
</script>

<div class="grid h-screen place-items-center">
	<div class="card w-96 bg-base-100 shadow-xl">
		{#if !claimed}
			<div class="card-body">
				<h2 class="card-title">Claim Your Spot!</h2>
				<p>Click "CLAIM" to secure your spot on the grid</p>
				<div class="card-actions justify-end">
					<button class="btn btn-secondary" on:click={claimYourSpot}>CLAIM</button>
				</div>
			</div>
		{:else if waiting}
			<div class="card-body">
				<h2 class="card-title">Claiming Spot</h2>
				<p>...</p>
			</div>
		{:else}
			<div class="card-body">
				<h2 class="card-title">You've Claimed Your Spot!</h2>
				<p>Congratulations! Look for the new pulsing spot on the grid</p>
				<a class="btn" href="/">View Grid</a>
			</div>
		{/if}
	</div>
</div>
