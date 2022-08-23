<script>
	import SVG from '$lib/SVG.svelte';
</script>

<div class="flex pt-16 p-8 flex-col xl:flex-row justify-center">
	<div class="xl:w-3/4">
		<SVG />
	</div>
	<div class="xl:w-1/4 mx-4">
		<div class="text-center text-6xl font-sans font-bold text-accent">
			The World's Most Collaborative NFT
		</div>
		<div class="flex justify-center pt-12 xl:pt-52"><img src="/qr.png" alt="qr code" /></div>
		<div class="flex justify-center pt-12 xl:pt-24 font-sans text-2xl">
			<span class="bg-secondary text-accent p-6">Scan To Participate</span>
		</div>
	</div>
</div>
