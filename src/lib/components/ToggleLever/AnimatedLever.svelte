<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';

	export let isOpen: boolean = true;

	let middleSegmentRef: SVGLineElement;

	onMount(() => {
		// Set initial state - open is upward (-45 degrees)
		if (isOpen) {
			gsap.set(middleSegmentRef, { rotation: -45, transformOrigin: 'left center' });
		} else {
			gsap.set(middleSegmentRef, { rotation: 0, transformOrigin: 'left center' });
		}
	});

	$: {
		if (middleSegmentRef) {
			if (isOpen) {
				// Open position: middle segment rotates up (-45 degrees)
				gsap.to(middleSegmentRef, {
					rotation: -45,
					transformOrigin: 'left center',
					duration: 0.6,
					ease: 'power2.inOut'
				});
			} else {
				// Closed position: middle segment is horizontal (0 degrees)
				gsap.to(middleSegmentRef, {
					rotation: 0,
					transformOrigin: 'left center',
					duration: 0.6,
					ease: 'power2.inOut'
				});
			}
		}
	}
</script>

<div class="flex items-center gap-4 p-8">
	<div class="flex items-center justify-center rounded-lg shadow-sm">
		<svg width="64" height="64" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
			<rect width="64" height="64" rx="8" fill="#E2E8F0" />
			<circle cx="32" cy="32" r="16" stroke="#94A3B8" stroke-width="2" fill="none" />
			<circle cx="32" cy="32" r="4" fill="#94A3B8" />
		</svg>
	</div>

	<div class="flex items-center justify-center">
		<svg width="140" height="100" viewBox="0 0 140 100" class="overflow-visible">
			<!-- First segment (static) -->
			<line
				x1="10"
				y1="50"
				x2="50"
				y2="50"
				stroke="#475569"
				stroke-width="8"
				stroke-linecap="round"
			/>
			<circle cx="10" cy="50" r="8" fill="#64748b" />

			<!-- Middle segment (animated) - starts at x=50 -->
			<g transform="translate(50, 50)">
				<line
					bind:this={middleSegmentRef}
					x1="0"
					y1="0"
					x2="40"
					y2="0"
					stroke="#3b82f6"
					stroke-width="8"
					stroke-linecap="round"
				/>
			</g>

			<!-- Third segment (static) - positioned based on middle segment -->
			<line
				x1="90"
				y1="50"
				x2="130"
				y2="50"
				stroke="#475569"
				stroke-width="8"
				stroke-linecap="round"
			/>
			<circle cx="130" cy="50" r="8" fill="#64748b" />

			<!-- Joint circles -->
			<circle cx="50" cy="50" r="8" fill="#64748b" />
			<circle cx="90" cy="50" r="8" fill="#64748b" />
		</svg>
	</div>

	<div class="flex items-center justify-center rounded-lg shadow-sm">
		<svg width="64" height="64" viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
			<rect width="64" height="64" rx="8" fill="#E2E8F0" />
			<rect x="16" y="16" width="32" height="32" rx="4" stroke="#94A3B8" stroke-width="2" fill="none" />
			<path d="M24 32L32 40L48 24" stroke="#94A3B8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
		</svg>
	</div>
</div>
