<script>
	import { AspectRatio } from "$lib/components/ui/aspect-ratio";

</script>

<div class="w-64 h-64 p-1 rounded-lg bg-gradient-to-r from-pink-500 via-red-500 to-yellow-500 animate-gradient-x">
	<AspectRatio ratio={1 / 1} class="bg-background">
		<img src="/img/user.png" alt="Animated border image" class="rounded-md object-cover w-full h-full" />
	</AspectRatio>
</div>

<style lang="postcss">
	@keyframes gradient-x {
		0%,
		100% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
	}
	.animate-gradient-x {
		animation: gradient-x 3s ease infinite;
		background-size: 200% 200%;
	}
</style>