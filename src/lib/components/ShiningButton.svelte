<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';

	let buttonRef: HTMLButtonElement;
	let shineRef: HTMLDivElement;

	onMount(() => {
		// Set up the shine element initial state
		gsap.set(shineRef, {
			rotation: 45,
			x: '-100%',
			opacity: 0
		});
	});

	function handleMouseEnter() {
		// Create a timeline for the shining effect
		const tl = gsap.timeline();

		tl.to(shineRef, {
			x: '200%',
			opacity: 1,
			duration: 0.6,
			ease: 'power2.inOut'
		}).to(shineRef, {
			opacity: 0,
			duration: 0.2
		}, '-=0.2');

		// Scale up the button slightly
		gsap.to(buttonRef, {
			scale: 1.05,
			duration: 0.3,
			ease: 'power2.out'
		});
	}

	function handleMouseLeave() {
		// Reset button scale
		gsap.to(buttonRef, {
			scale: 1,
			duration: 0.3,
			ease: 'power2.out'
		});

		// Reset shine position
		gsap.set(shineRef, {
			x: '-100%',
			opacity: 0
		});
	}

	function handleClick() {
		// Shrink and grow back animation
		gsap.timeline()
			.to(buttonRef, {
				scale: 0.95,
				duration: 0.1,
				ease: 'power2.out'
			})
			.to(buttonRef, {
				scale: 1.05,
				duration: 0.2,
				ease: 'power2.out'
			});
	}
</script>

<button
	bind:this={buttonRef}
	on:mouseenter={handleMouseEnter}
	on:mouseleave={handleMouseLeave}
	on:click={handleClick}
	class="relative px-8 py-4 text-lg font-semibold text-white bg-gradient-to-br from-blue-800 to-blue-500 border-none rounded-lg cursor-pointer overflow-hidden shadow-md transition-shadow duration-300 hover:shadow-[0_10px_20px_rgba(59,130,246,0.4)]"
>
	<span class="relative z-[2]">
		<slot>Hover Me</slot>
	</span>
	<div bind:this={shineRef} class="absolute -top-1/2 left-0 w-[30%] h-[200%] bg-gradient-to-r from-transparent via-white/80 to-transparent pointer-events-none z-[1]"></div>
</button>
