<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	onMount(() => {
		gsap.to('.c', {
            scrollTrigger: {
                trigger: '.c',
                toggleActions: 'restart pause reverse none',
                
            },
			x: 400,
			rotation: 360,
			duration: 3
		});
	});
</script>

<section class="p-6 min-h-[500dvh]">
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
