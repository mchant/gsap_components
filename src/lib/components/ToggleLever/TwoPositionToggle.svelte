<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import { gsap } from 'gsap';

	export let isOn: boolean = false;

	const dispatch = createEventDispatcher<{ change: boolean }>();

	let knobRef: HTMLDivElement;

	function toggle() {
		isOn = !isOn;
		dispatch('change', isOn);

		// Animate knob
		// Total width: 80px, knob width: 32px, padding: 4px each side
		// ON position: 80 - 32 - 4 - 4 = 40px translation
		gsap.to(knobRef, {
			x: isOn ? 40 : 0,
			duration: 0.3,
			ease: 'power2.out'
		});
	}
</script>

<button
	class="relative w-20 h-10 border-none rounded-full cursor-pointer transition-colors duration-300 overflow-hidden"
	class:bg-slate-200={!isOn}
	class:bg-blue-300={isOn}
	on:click={toggle}
	aria-label="Toggle switch"
>
	<div bind:this={knobRef} class="absolute top-1 left-1 w-8 h-8 bg-gradient-to-br from-blue-500 to-blue-800 rounded-full shadow-md z-[2]"></div>
	<span
		class="absolute top-1/2 -translate-y-1/2 left-2 text-xs font-bold z-[1] select-none transition-colors"
		class:text-slate-500={!isOn}
		class:text-slate-400={isOn}
	>OFF</span>
	<span
		class="absolute top-1/2 -translate-y-1/2 right-2 text-xs font-bold z-[1] select-none transition-colors"
		class:text-blue-800={!isOn}
		class:text-blue-900={isOn}
	>ON</span>
</button>
