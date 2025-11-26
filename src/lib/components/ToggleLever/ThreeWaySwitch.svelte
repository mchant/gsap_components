<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import { gsap } from 'gsap';

	export let position: 1 | 2 | 3 = 1;

	const dispatch = createEventDispatcher<{ change: 1 | 2 | 3 }>();

	let switchRef: HTMLDivElement;
	let knobRef: HTMLDivElement;

	function setPosition(newPosition: 1 | 2 | 3) {
		if (newPosition === position) return;

		position = newPosition;
		dispatch('change', position);

		// Animate knob to new position
		const positions = {
			1: '0.25rem',
			2: 'calc(33.333% + 0.125rem)',
			3: 'calc(66.666% + 0.0rem)'
		};

		gsap.to(knobRef, {
			left: positions[position],
			duration: 0.3,
			ease: 'power2.out'
		});
	}

	function handleClick(pos: 1 | 2 | 3) {
		setPosition(pos);
	}
</script>

<div class="flex justify-center">
	<div bind:this={switchRef} class="relative flex bg-slate-200 rounded-full p-1 w-[300px] h-[60px]">
		<div bind:this={knobRef} class="absolute top-1 left-1 w-[calc(33.333%-0.25rem)] h-[calc(100%-0.5rem)] bg-gradient-to-br from-blue-500 to-blue-800 rounded-[1.75rem] shadow-md z-[1]"></div>
		<button class="flex-1 bg-transparent border-none cursor-pointer relative z-[2] font-semibold text-sm text-slate-500 hover:text-slate-800 transition-colors" on:click={() => handleClick(1)} aria-label="Position 1">
			<span class="relative z-[3] mix-blend-difference text-white">StandBy</span>
		</button>
		<button class="flex-1 bg-transparent border-none cursor-pointer relative z-[2] font-semibold text-sm text-slate-500 hover:text-slate-800 transition-colors" on:click={() => handleClick(2)} aria-label="Position 2">
			<span class="relative z-[3] mix-blend-difference text-white">Charging</span>
		</button>
		<button class="flex-1 bg-transparent border-none cursor-pointer relative z-[2] font-semibold text-sm text-slate-500 hover:text-slate-800 transition-colors" on:click={() => handleClick(3)} aria-label="Position 3">
			<span class="relative z-[3] mix-blend-difference text-white">Discharging</span>
		</button>
	</div>
</div>
