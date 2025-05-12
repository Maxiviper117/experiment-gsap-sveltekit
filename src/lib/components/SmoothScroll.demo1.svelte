<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { ScrollSmoother } from 'gsap/ScrollSmoother';

	gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

	onMount(() => {
		let smooth = ScrollSmoother.create({});

		smooth.effects('img', { speed: 'auto',lag: 0.5,effectsPadding: 2 });
	});
</script>

<section class="flex min-h-[300dvh] flex-col justify-center bg-stone-900 py-20">
	<div class="container mx-auto flex flex-col gap-20" id="smooth-content">
		<div class="image_cont">
			<img src="https://picsum.photos/seed/picsum/800/600" alt="Rando 1" />
		</div>
		<div class="image_cont">
			<img src="https://picsum.photos/seed/picsum/800/600" alt="Rando 1" />
		</div>
		<div class="image_cont">
			<img src="https://picsum.photos/seed/picsum/800/600" alt="Rando 1" />
		</div>
		<div class="image_cont">
			<img src="https://picsum.photos/seed/picsum/800/600" alt="Rando 1" />
		</div>
	</div>
</section>

<style>
	.image_cont {
		position: relative;
		overflow: hidden;
		height: 60vh;
		max-height: 500px;
	}

	img {
		position: absolute;
		width: 100%;
		height: 160%;
		object-fit: cover;
		bottom: 0;
	}
</style>
