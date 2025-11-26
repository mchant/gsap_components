<script lang="ts">
	import ShiningButton from '$lib/components/ShiningButton.svelte';
	import SwitchControlledCard from '$lib/components/SwitchControlledCard/SwitchControlledCard.svelte';
	import ToggleLever from '$lib/components/ToggleLever/ToggleLever.svelte';
	import BatterySlider from '$lib/components/BatterySlider/BatterySlider.svelte';
</script>

<svelte:head>
	<title>GSAP Components Showcase</title>
</svelte:head>

<main class="min-h-screen flex items-center justify-center p-8 bg-gradient-to-br from-indigo-500 to-purple-600">
	<div class="max-w-3xl w-full text-center">
		<h1 class="text-5xl font-extrabold text-white m-0 mb-4 drop-shadow-lg">GSAP Components Showcase</h1>
		<p class="text-xl text-white/90 m-0 mb-12">Interactive components powered by GSAP animations</p>

		<section class="bg-white rounded-2xl p-8 shadow-[0_20px_60px_rgba(0,0,0,0.3)] mb-8">
			<h2 class="text-3xl text-slate-800 m-0 mb-2">Shining Button</h2>
			<p class="text-slate-500 m-0 mb-8">Hover over the button to see the shining effect animation</p>

			<div class="flex justify-center items-center min-h-[150px]">
				<ShiningButton>Hover Me</ShiningButton>
			</div>
		</section>

		<section class="bg-white rounded-2xl p-8 shadow-[0_20px_60px_rgba(0,0,0,0.3)] mb-8">
			<h2 class="text-3xl text-slate-800 m-0 mb-2">Switch-Controlled Card</h2>
			<p class="text-slate-500 m-0 mb-8">
				Use the 3-way switch to control the dot animation: Stop, Clockwise, or Counter-Clockwise
			</p>

			<div class="flex justify-center items-center min-h-[150px]">
				<SwitchControlledCard />
			</div>
		</section>

		<section class="bg-white rounded-2xl p-8 shadow-[0_20px_60px_rgba(0,0,0,0.3)] mb-8">
			<h2 class="text-3xl text-slate-800 m-0 mb-2">Toggle Lever</h2>
			<p class="text-slate-500 m-0 mb-8">
				Toggle the switch to open or close the lever between the images
			</p>

			<div class="flex justify-center items-center min-h-[150px]">
				<ToggleLever />
			</div>
		</section>

		<section class="bg-white rounded-2xl p-8 shadow-[0_20px_60px_rgba(0,0,0,0.3)] mb-8">
			<h2 class="text-3xl text-slate-800 m-0 mb-2">Battery Slider</h2>
			<p class="text-slate-500 m-0 mb-8">
				Drag the slider to charge or drain the battery
			</p>

			<div class="flex justify-center items-center min-h-[150px]">
				<BatterySlider />
			</div>
		</section>
	</div>
</main>
