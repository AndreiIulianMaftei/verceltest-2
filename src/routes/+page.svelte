<script lang="ts">
	import { onMount, onDestroy } from "svelte";
	import confetti from "canvas-confetti";
	import { Button } from "$lib/components/ui/button";
	import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from "$lib/components/ui/card";
	import { Separator } from "$lib/components/ui/separator";
	import { fly } from "svelte/transition";
	import pfp from "$lib/img/user.png";
	import tumLogo from "$lib/img/tum-logo.png";

	let confettiCanvas: HTMLCanvasElement;
	let myConfetti: confetti.CreateTypes;
	let showMoreButton = false;

	onMount(() => {
		myConfetti = confetti.create(confettiCanvas, {
			resize: true,
			useWorker: true,
		});

		fireFullScreenConfetti();

		setTimeout(() => {
			showMoreButton = true;
		}, 2000);
	});

	onDestroy(() => {
		if (myConfetti) {
			myConfetti.reset();
		}
	});

	function fireFullScreenConfetti() {
		if (myConfetti) {
			const duration = 5 * 1000;
			const animationEnd = Date.now() + duration;
			const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

			function randomInRange(min: number, max: number) {
				return Math.random() * (max - min) + min;
			}

			const interval: any = setInterval(function () {
				const timeLeft = animationEnd - Date.now();

				if (timeLeft <= 0) {
					return clearInterval(interval);
				}

				const particleCount = 50 * (timeLeft / duration);

				myConfetti(
					Object.assign({}, defaults, {
						particleCount,
						origin: { x: randomInRange(0.1, 0.9), y: Math.random() - 0.2 },
					})
				);
				myConfetti(
					Object.assign({}, defaults, {
						particleCount,
						origin: { x: randomInRange(0.1, 0.9), y: Math.random() - 0.2 },
					})
				);
			}, 250);
		}
	}

	function fireConfetti() {
		if (myConfetti) {
			myConfetti({
				particleCount: 100,
				spread: 70,
				origin: { y: 0.6 },
				gravity: 1,
				ticks: 300,
				colors: ["#0065BD", "#3070B3", "#98C6EA", "#64A0C8", "#A2BAD2"],
				shapes: ["square", "circle"],
				scalar: 1.2,
			});
		}
	}
</script>

<div class="min-h-screen bg-gradient-to-br from-[#0065BD] to-[#98C6EA] flex flex-col items-center justify-center p-4 relative overflow-hidden">
	<canvas bind:this={confettiCanvas} class="fixed inset-0 pointer-events-none w-full h-full" />

	<Card class="w-full max-w-5xl bg-white/10 backdrop-blur-md shadow-xl relative z-10">
		<CardContent class="p-6">
			<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
				<!-- First Column: Profile -->
				<div class="flex flex-col items-center text-center">
					<div class="w-36 h-36 md:w-48 md:h-48 rounded-full overflow-hidden mb-4 border-4 border-[#0065BD] shadow-lg">
						<img src={pfp} alt="" class="w-full h-full object-cover" />
					</div>
					<h2 class="text-xl md:text-2xl font-bold text-white mb-2">John Doe</h2>
					<p class="text-base md:text-lg text-gray-200 mb-4">Information Engineering Student</p>
					<img src={tumLogo} alt="" class="w-20 md:w-24 mb-2" />
					<p class="text-xs md:text-sm text-gray-300">Technical University of Munich</p>
				</div>

				<!-- Second Column: Experience -->
				<div>
					<Card class="h-full bg-white/5 border-none">
						<CardHeader>
							<CardTitle class="text-lg md:text-xl text-white">Experience</CardTitle>
						</CardHeader>
						<CardContent>
							<ul class="space-y-3 md:space-y-4 text-sm md:text-base text-gray-200">
								<li>
									<h3 class="font-semibold">Research Assistant</h3>
									<p class="text-xs md:text-sm">TUM Institute of AI • 2022 - Present</p>
								</li>
								<li>
									<h3 class="font-semibold">Software Engineering Intern</h3>
									<p class="text-xs md:text-sm">Tech Innovations GmbH • Summer 2021</p>
								</li>
								<li>
									<h3 class="font-semibold">Student Project Lead</h3>
									<p class="text-xs md:text-sm">TUM Robotics Club • 2020 - 2021</p>
								</li>
							</ul>
						</CardContent>
					</Card>
				</div>

				<!-- Third Column: About Me -->
				<div>
					<Card class="h-full bg-white/5 border-none">
						<CardHeader>
							<CardTitle class="text-lg md:text-xl text-white">About Me</CardTitle>
						</CardHeader>
						<CardContent>
							<p class="text-sm md:text-base text-gray-200">As an Information Engineering student at TUM, I'm passionate about leveraging technology to solve complex problems. My journey in tech has been driven by curiosity and a desire to make a positive impact.</p>
							<p class="text-sm md:text-base text-gray-200 mt-3 md:mt-4">Outside of my studies, I enjoy participating in hackathons, contributing to open-source projects, and exploring the beautiful Bavarian landscapes. I'm always eager to learn and collaborate on innovative projects that push the boundaries of what's possible in tech.</p>
						</CardContent>
					</Card>
				</div>
			</div>
		</CardContent>
		<CardFooter class="flex justify-center space-x-3 md:space-x-4 pt-4">
			<Button variant="outline" class="bg-[#0065BD] text-white hover:bg-[#3070B3] text-xs md:text-sm">
				<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1 md:mr-2 h-3 w-3 md:h-4 md:w-4">
					<path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path>
					<rect width="4" height="12" x="2" y="9"></rect>
					<circle cx="4" cy="4" r="2"></circle>
				</svg>
				LinkedIn
			</Button>
			<Button variant="outline" class="bg-gray-700 text-white hover:bg-gray-800 text-xs md:text-sm" >
				<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1 md:mr-2 h-3 w-3 md:h-4 md:w-4"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
				GitHub
			</Button>
		</CardFooter>
	</Card>

	{#if showMoreButton}
		<div transition:fly={{ y: 20, duration: 800, delay: 300 }} class="mt-4">
			<button class="text-gray-200 hover:text-white transition-colors duration-300 flex items-center group">
				<span class="mr-2 text-xs md:text-sm font-medium">More About My Story</span>
				<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-3 w-3 md:h-4 md:w-4 transform group-hover:translate-x-1 transition-transform duration-300">
					<path d="M5 12h14" />
					<path d="m12 5 7 7-7 7" />
				</svg>
			</button>
		</div>
	{/if}
</div>

<style>
	:global(body) {
		background-color: #0065bd;
		color: #ffffff;
	}

	.min-h-screen {
		min-height: 100vh;
	}

	.bg-gradient-to-br {
		background-image: linear-gradient(to bottom right, var(--tw-gradient-stops));
	}

	.from-\[\#0065BD\] {
		--tw-gradient-from: #0065bd;
		--tw-gradient-stops: var(--tw-gradient-from), var(--tw-gradient-to, rgba(0, 101, 189, 0));
	}

	.to-\[\#98C6EA\] {
		--tw-gradient-to: #98c6ea;
	}

	.backdrop-blur-md {
		backdrop-filter: blur(12px);
	}

	.bg-white\/10 {
		background-color: rgba(255, 255, 255, 0.1);
	}

	.shadow-xl {
		box-shadow:
			0 20px 25px -5px rgba(0, 0, 0, 0.1),
			0 10px 10px -5px rgba(0, 0, 0, 0.04);
	}

	.transition-all {
		transition-property: all;
		transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
		transition-duration: 150ms;
	}

	.duration-300 {
		transition-duration: 300ms;
	}

	.group:hover .group-hover\:translate-x-1 {
		transform: translateX(0.25rem);
	}

	@media (max-width: 640px) {
		.card {
			padding: 1rem;
		}
	}

	@media (min-width: 641px) and (max-width: 1024px) {
		.card {
			padding: 1.5rem;
		}
	}

	@media (min-width: 1025px) {
		.card {
			padding: 2rem;
		}
	}
</style>