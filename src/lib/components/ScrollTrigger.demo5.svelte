<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { browser } from '$app/environment';

	gsap.registerPlugin(ScrollTrigger);

	onMount(() => {
		if (!browser) return;

		gsap.defaults({ ease: 'none', duration: 2 });

		const container = document.querySelector('section.container') as HTMLElement;
		const panels = gsap.utils.toArray<HTMLElement>('.panel');

		// use the actual rendered height of a panel (100dvh in your CSS)
		const panelHeight = panels[0].offsetHeight;

		gsap.to(panels, {
			yPercent: -100 * (panels.length - 1),
			scrollTrigger: {
				trigger: container,
				pin: true,
				scrub: 1,
				snap: 1 / (panels.length - 1),
				anticipatePin: 1,
				invalidateOnRefresh: true, // recalculates on resize / orientation-change
				end: () => `+=${panelHeight * (panels.length - 1)}`
			}
		});
	});
</script>

<section class="container">
	<div class="panel p1 bg-red-500">One</div>
	<div class="panel p2 bg-blue-500">Two</div>
	<div class="panel p3 bg-green-500">Three</div>
	<div class="panel p4 bg-purple-500">Four</div>
</section>

<style>
	/* html disable vertial scrolling */
	html {
		overflow-y: hidden;
	}
	.panel {
		width: 100dvw;
		height: 100dvh;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 2rem;
		color: white;
	}
	.container {
		position: relative;
	}
</style>
