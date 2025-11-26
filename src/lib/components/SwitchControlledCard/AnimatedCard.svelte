<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';

	export let animationState: 1 | 2 | 3 = 1; // 1 = stop, 2 = clockwise, 3 = counter-clockwise
	export let speed: number = 100; // 0-100

	let cardRef: HTMLDivElement;
	let dotRefs: HTMLDivElement[] = [];
	let clockwiseAnimations: gsap.core.Tween[] = [];
	let counterClockwiseAnimations: gsap.core.Tween[] = [];

	const numDots = 8;

	onMount(() => {
		setupAnimations();
	});

	function setupAnimations() {
		// Get card dimensions
		const rect = cardRef.getBoundingClientRect();
		const width = rect.width;
		const height = rect.height;
		const perimeter = 2 * (width + height);
		const dotSize = 12;
		const dotOffset = dotSize / 2; // Center the dot on the border

		// Calculate positions along the perimeter for clockwise movement
		function getPositionClockwise(progress: number) {
			const distance = progress * perimeter;

			if (distance < width) {
				// Top edge: left to right
				return { x: distance - dotOffset, y: -dotOffset };
			} else if (distance < width + height) {
				// Right edge: top to bottom
				return { x: width - dotOffset, y: distance - width - dotOffset };
			} else if (distance < 2 * width + height) {
				// Bottom edge: right to left
				return { x: width - (distance - width - height) - dotOffset, y: height - dotOffset };
			} else {
				// Left edge: bottom to top
				return { x: -dotOffset, y: height - (distance - 2 * width - height) - dotOffset };
			}
		}

		// Calculate positions for counter-clockwise movement
		function getPositionCounterClockwise(progress: number) {
			const distance = progress * perimeter;

			if (distance < height) {
				// Left edge: top to bottom
				return { x: -dotOffset, y: distance - dotOffset };
			} else if (distance < width + height) {
				// Bottom edge: left to right
				return { x: distance - height - dotOffset, y: height - dotOffset };
			} else if (distance < width + 2 * height) {
				// Right edge: bottom to top
				return { x: width - dotOffset, y: height - (distance - width - height) - dotOffset };
			} else {
				// Top edge: right to left
				return { x: width - (distance - width - 2 * height) - dotOffset, y: -dotOffset };
			}
		}

		dotRefs.forEach((dot, index) => {
			const offset = index / numDots;

			// Create clockwise animation
			const startPosClockwise = getPositionClockwise(offset);
			gsap.set(dot, { x: startPosClockwise.x, y: startPosClockwise.y });

			const cwTween = gsap.to(dot, {
				duration: 4,
				repeat: -1,
				ease: 'none',
				paused: true,
				onUpdate: function() {
					const progress = (this.progress() + offset) % 1;
					const pos = getPositionClockwise(progress);
					gsap.set(dot, { x: pos.x, y: pos.y });
				}
			});
			clockwiseAnimations.push(cwTween);

			// Create counter-clockwise animation
			const ccwTween = gsap.to(dot, {
				duration: 4,
				repeat: -1,
				ease: 'none',
				paused: true,
				onUpdate: function() {
					const progress = (this.progress() + offset) % 1;
					const pos = getPositionCounterClockwise(progress);
					gsap.set(dot, { x: pos.x, y: pos.y });
				}
			});
			counterClockwiseAnimations.push(ccwTween);
		});
	}

	$: {
		if (clockwiseAnimations.length > 0 && counterClockwiseAnimations.length > 0) {
			if (animationState === 1) {
				// Stop
				clockwiseAnimations.forEach(anim => anim.pause());
				counterClockwiseAnimations.forEach(anim => anim.pause());
			} else if (animationState === 2) {
				// Clockwise
				counterClockwiseAnimations.forEach(anim => anim.pause());
				clockwiseAnimations.forEach(anim => anim.play());
			} else if (animationState === 3) {
				// Counter-clockwise
				clockwiseAnimations.forEach(anim => anim.pause());
				counterClockwiseAnimations.forEach(anim => anim.play());
			}
		}
	}

	$: {
		if (clockwiseAnimations.length > 0 && counterClockwiseAnimations.length > 0) {
			const timeScale = speed / 100;
			clockwiseAnimations.forEach(anim => anim.timeScale(timeScale));
			counterClockwiseAnimations.forEach(anim => anim.timeScale(timeScale));
		}
	}
</script>

<div class="relative inline-block">
	<div bind:this={cardRef} class="bg-white rounded-2xl p-8 shadow-md border-2 border-slate-200 min-w-[300px]">
		<div class="flex justify-center mb-4">
			<svg width="64" height="64" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
				<rect width="64" height="64" rx="8" fill="#E2E8F0" />
				<path
					d="M20 44L28 36L36 44L44 28"
					stroke="#94A3B8"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
				/>
				<circle cx="38" cy="26" r="3" fill="#94A3B8" />
			</svg>
		</div>
		<div>
			<h3 class="m-0 mb-2 text-slate-800 text-xl">Card with Image</h3>
			<p class="m-0 text-slate-500 text-sm">This is a placeholder card with an animated border.</p>
		</div>
	</div>

	{#each Array(numDots) as _, i}
		<div bind:this={dotRefs[i]} class="absolute w-3 h-3 bg-gradient-to-br from-blue-500 to-blue-800 rounded-full shadow-[0_2px_4px_rgba(59,130,246,0.4)] top-0 left-0 pointer-events-none"></div>
	{/each}
</div>
