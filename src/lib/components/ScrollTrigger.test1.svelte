<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { ScrollSmoother } from 'gsap/ScrollSmoother';

	gsap.registerPlugin(ScrollTrigger, ScrollSmoother);

	onMount(() => {
		ScrollSmoother.create({
			wrapper: '#smooth-wrapper',
			content: '#smooth-content',
			smooth: 2,
		});
		gsap.set('.b', {
			xPercent: -100
		});
		gsap.to('.b', {
			scrollTrigger: {
				trigger: '.b',
				start: 'top bottom-=50',
				end: 'top bottom-=300',
				// markers: true,
				scrub: 0.5,
				toggleActions: 'play none none none'
			},
			xPercent: 0,
			duration: 1
		});
		gsap.utils.toArray<HTMLElement>('.c').forEach((el) => {
			gsap.set(el, {
				y: 100,
				scale: 0.8,
				opacity: 0,
				rotationX: -5
			});
			gsap.to(el, {
				scrollTrigger: {
					trigger: el,
					start: 'top bottom-=50',
					end: 'top bottom-=300',
					// markers: true,
					scrub: true
				},
				y: 0,
				scale: 1,
				opacity: 1,
				rotationX: 0,
				transformOrigin: 'center center',
				duration: 1
			});
		});
	});
</script>

<section id="smooth-wrapper" class="flex min-h-[500dvh] flex-col gap-30 p-6">
	<div class="container mx-auto flex flex-col gap-300 perspective-[800px]" id="smooth-content">
		<div class="box a">a</div>
		<div class="box b">b</div>
		<div class="box c rounded-3xl shadow-2xl outline-2 -outline-offset-1 outline-gray-500/10">
			<img
				src="https://picsum.photos/seed/picsum/1200/1200"
				alt="Random"
				class="h-full w-full rounded-3xl object-cover"
			/>
		</div>
		<div class="box c rounded-3xl shadow-2xl outline-1 -outline-offset-1 outline-gray-500/25">
			<img
				src="https://picsum.photos/seed/picsum/1200/1200"
				alt="Random"
				class="h-full w-full rounded-3xl object-cover"
			/>
		</div>
		<div class="box c rounded-3xl shadow-2xl outline-1 -outline-offset-1 outline-gray-500/25">
			<img
				src="https://picsum.photos/seed/picsum/1200/1200"
				alt="Random"
				class="h-full w-full rounded-3xl object-cover"
			/>
		</div>
		<div class="box c rounded-3xl shadow-2xl outline-1 -outline-offset-1 outline-gray-500/25">
			<img
				src="https://picsum.photos/seed/picsum/1200/1200"
				alt="Random"
				class="h-full w-full rounded-3xl object-cover"
			/>
		</div>
	</div>
</section>

<style>
	.box {
		width: 100%;
		height: 500px;

		&.a {
			background-color: rgb(190, 190, 190);
		}

		&.b {
			background-color: green;
		}

		/* &.c {
			background-color: blue;
		} */
	}
</style>
