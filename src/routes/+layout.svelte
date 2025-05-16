<script lang="ts">
	import '../app.css';

	let { children } = $props();

	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollSmoother } from 'gsap/ScrollSmoother';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { Flip } from 'gsap/Flip';

	onMount(() => {
		gsap.registerPlugin(ScrollSmoother, ScrollTrigger, Flip);
		ScrollSmoother.create({
			wrapper: '#smooth-wrapper',
			content: '#smooth-content',
			smooth: 3, // adjust smoothing factor
			effects: true, // enable data-speed/data-lag effects
			smoothTouch: 0.1 // optional touch smoothing
		});
	});
</script>

<div id="smooth-wrapper">
	<main id="smooth-content">
		{@render children()}
	</main>
</div>
