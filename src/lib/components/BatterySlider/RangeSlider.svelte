<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let value: number = 50;

	const dispatch = createEventDispatcher<{ change: number }>();

	function handleInput(event: Event) {
		const target = event.target as HTMLInputElement;
		value = Number(target.value);
		dispatch('change', value);
	}
</script>

<div class="flex flex-col items-center gap-4 w-full max-w-md">
	<div class="flex justify-between w-full text-slate-600 font-semibold">
		<span>0</span>
		<span class="text-2xl text-blue-600">{value}%</span>
		<span>100</span>
	</div>
	<input
		type="range"
		min="0"
		max="100"
		{value}
		on:input={handleInput}
		class="w-full h-2 bg-slate-200 rounded-lg appearance-none cursor-pointer [&::-webkit-slider-thumb]:appearance-none [&::-webkit-slider-thumb]:w-6 [&::-webkit-slider-thumb]:h-6 [&::-webkit-slider-thumb]:bg-gradient-to-br [&::-webkit-slider-thumb]:from-blue-500 [&::-webkit-slider-thumb]:to-blue-800 [&::-webkit-slider-thumb]:rounded-full [&::-webkit-slider-thumb]:cursor-pointer [&::-webkit-slider-thumb]:shadow-md [&::-moz-range-thumb]:w-6 [&::-moz-range-thumb]:h-6 [&::-moz-range-thumb]:bg-gradient-to-br [&::-moz-range-thumb]:from-blue-500 [&::-moz-range-thumb]:to-blue-800 [&::-moz-range-thumb]:rounded-full [&::-moz-range-thumb]:cursor-pointer [&::-moz-range-thumb]:shadow-md [&::-moz-range-thumb]:border-0"
	/>
</div>
