<script lang="ts">
	import { gsap } from 'gsap';

	export let chargeLevel: number = 50; // 0-100

	let fillRef: HTMLDivElement;

	// Get fill color based on charge level
	function getFillColor(level: number): string {
		if (level <= 20) return 'bg-red-500';
		if (level <= 50) return 'bg-yellow-500';
		return 'bg-green-500';
	}

	$: fillColor = getFillColor(chargeLevel);

	$: {
		if (fillRef) {
			gsap.to(fillRef, {
				height: `${chargeLevel}%`,
				duration: 0.5,
				ease: 'power2.out'
			});
		}
	}
</script>

<div class="flex flex-col items-center gap-4">
	<!-- Battery terminal at top -->
	<div class="w-12 h-4 bg-slate-400 rounded-t-md"></div>

	<!-- Battery body -->
	<div class="relative w-32 h-48 bg-slate-200 rounded-lg border-4 border-slate-400 overflow-hidden flex flex-col-reverse -mt-4">
		<!-- Battery fill (fills from bottom to top) -->
		<div
			bind:this={fillRef}
			class="w-full transition-colors duration-300 {fillColor}"
			style="height: {chargeLevel}%"
		></div>
	</div>

	<!-- Charge level text -->
	<div class="text-slate-700 font-bold text-lg">
		{#if chargeLevel <= 20}
			Low Battery
		{:else if chargeLevel <= 50}
			Medium Charge
		{:else if chargeLevel < 100}
			Good Charge
		{:else}
			Fully Charged
		{/if}
	</div>
</div>
