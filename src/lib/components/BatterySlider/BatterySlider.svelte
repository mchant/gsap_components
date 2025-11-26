<script lang="ts">
	import RangeSlider from './RangeSlider.svelte';
	import AnimatedBattery from './AnimatedBattery.svelte';

	let chargeLevel: number = 50;

	function handleSliderChange(event: CustomEvent<number>) {
		chargeLevel = event.detail;
	}
</script>

<div class="flex flex-col items-center gap-8">
	<AnimatedBattery {chargeLevel} />
	<RangeSlider value={chargeLevel} on:change={handleSliderChange} />
</div>
