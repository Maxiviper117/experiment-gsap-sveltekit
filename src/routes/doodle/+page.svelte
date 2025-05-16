<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { ScrollSmoother } from 'gsap/ScrollSmoother';
	import { Flip } from 'gsap/Flip';
	import type { Attachment } from 'svelte/attachments';

	function swap([a, b]) {
		a.parentNode.children[0] === a ? a.parentNode.appendChild(a) : a.parentNode.appendChild(b);
	}
	function doFlip() {
		// FLIP stands for First, Last, Invert, Play
		const imgs = gsap.utils.toArray('.imgs') as HTMLElement[];
		const state = Flip.getState(imgs); // FIRST - Get the state of the elements

		swap(imgs); // LAST - Swap the elements in the DOM

		Flip.from(state, {
			duration: 2,
			ease: 'power1.inOut'
		}); // INVERT - Invert the state
		// PLAY - Play the animation
	}

	onMount(() => {
		// Register GSAP plugins
		gsap.registerPlugin(ScrollTrigger, Flip);
	});

	const circleReveal: Attachment = (element) => {
		// console.log(element.nodeName); // 'DIV'
		console.log(element); // <div>...</div>
		let an = gsap.fromTo(
			element,
			{
				opacity: 0,
				clipPath: 'circle(0% at 50% 50%)'
			}, // Initial state
			{
				opacity: 1,
				clipPath: 'circle(75% at 50% 50%)', // Final state
				scrollTrigger: {
					trigger: element,
					start: 'top bottom-=200', // Start animation when the element enters the viewport
					end: '200% bottom-=200', // End animation when the element reaches the center
					// markers: true, 
					scrub: true 
				}
			}
		);

		return () => {
			an.kill(); // Cleanup animation on unmount
		};
	};

	onMount(() => {
		const ctx = gsap.context(() => {
			gsap
				.timeline({
					scrollTrigger: {
						trigger: '.pin-container',
						start: 'center center',
						end: (self) => `+=${self.trigger.offsetHeight}`, // Pin for full height of container
						// markers: true,
						scrub: 1,
						pin: true,
						snap: [1, 1] // Snap to the nearest section
					}
				})
				.fromTo(
					'img',
					{ opacity: 0, x: -100, y: 200, rotate: -10 },
					{ opacity: 1, x: 0, y: 0, rotate: 0, duration: 2 }
				)
				.fromTo('#content', { opacity: 0, y: 100 }, { opacity: 1, y: 0, duration: 1 }, '<0.5');
		});

		// Cleanup GSAP context on component unmount
		return () => {
			ctx.revert();
		};
	});
</script>

<section class="min-h-screen"></section>
<section class="min-h-screen">
	<div class="container mx-auto">
		<div class="pin-container flex flex-col items-center border border-red-200 py-20">
			<div id="content">
				<h2 class="mt-10 mb-5 text-center text-3xl font-bold text-gray-800">
					A Paradigm Shift in OnePlus Wearables
				</h2>
				<p class="mb-10 text-center text-lg text-gray-600">
					Stands as a testament to our Never Settle spirit, OnePlus Watch 3 boasting a 5-day battery
					life, enhanced display, and more precise dual-frequency GPS. It seamlessly integrates
					wellness monitoring, helping you manage your physical and emotional health and well-being.
				</p>
			</div>

			<img
				class="w-92 self-center rounded shadow"
				src="https://picsum.photos/seed/picsum/600/600"
				alt="Random Picsum"
			/>
		</div>
	</div>
</section>
<section class="py-60">
	<div class="container mx-auto">
		<div class=" border border-red-300" {@attach circleReveal}>
			<h3 class="mb-4 text-center text-5xl font-semibold uppercase">
				Built strong to last a lifetime
			</h3>
		</div>
	</div>
</section>
<section class="min-h-screen"></section>
<section class="min-h-screen">
	<div class="container mx-auto bg-red-200">
		<div
			class="grid grid-cols-[repeat(2,1fr)] place-items-center justify-center gap-4 bg-amber-100"
		>
			<img
				id="img1"
				class="imgs w-92 self-center rounded shadow"
				src="https://picsum.photos/seed/picsum/600/600"
				alt="Random Picsum"
			/>
			<img
				id="img2"
				class="imgs w-92 self-center rounded shadow"
				src="https://picsum.photos/seed/picsumm/600/600"
				alt="Random Picsum"
			/>
		</div>
		<button
			class="mt-10 rounded bg-blue-500 px-4 py-2 text-white hover:bg-blue-600"
			onclick={doFlip}>Do Flip</button
		>
	</div>
</section>
<section class="min-h-screen"></section>

<style>
	.pin-container {
		isolation: isolate;
	}
</style>
