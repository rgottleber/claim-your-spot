<script>
	import SVG from '$lib/SVG.svelte';
</script>

<div class="flex pt-16 p-8">
	<div class="w-3/4">
		<SVG />
	</div>
	<div class="w-1/4 flex-col justify-center">
		<div class="text-center text-6xl font-sans font-bold text-accent">
			The World's Most Collaborative NFT
		</div>
		<div class="flex justify-center pt-52"><img src="/qr.png" alt="qr code" /></div>
		<div class="flex justify-center pt-24 font-sans text-2xl">
			<span class="bg-secondary text-accent p-6">Scan To Participate</span>
		</div>
	</div>
</div>
