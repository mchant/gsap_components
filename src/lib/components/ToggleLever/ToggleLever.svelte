<script lang="ts">
	import TwoPositionToggle from './TwoPositionToggle.svelte';
	import AnimatedLever from './AnimatedLever.svelte';

	let isOn: boolean = false;

	function handleToggleChange(event: CustomEvent<boolean>) {
		isOn = event.detail;
	}
</script>

<div class="flex flex-col items-center gap-8">
	<TwoPositionToggle {isOn} on:change={handleToggleChange} />
	<AnimatedLever isOpen={!isOn} />
</div>
