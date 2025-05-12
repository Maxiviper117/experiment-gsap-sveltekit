<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { browser } from '$app/environment';

	gsap.registerPlugin(ScrollTrigger);

	onMount(() => {
		if (browser) {
			gsap.to('.c', {
				scrollTrigger: {
					trigger: '.c',
					start: 'top center',
					end: 'top 100px',
					scrub: true,
					pin: true,
					markers: true
				},
				x: 400,
				rotation: 360,
				duration: 3
			});
		}
	});
</script>

<section class="min-h-[500dvh] p-6">
	<div class="flex flex-col gap-300">
		<div class="box a">a</div>
		<div class="box b">b</div>
		<div class="box c">c</div>
	</div>
</section>

<style>
	.box {
		width: 100px;
		height: 100px;

		&.a {
			background-color: red;
		}

		&.b {
			background-color: green;
		}

		&.c {
			background-color: blue;
		}
	}
</style>
