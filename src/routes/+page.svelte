<script module>
	const images = [
		'images/1331453.png',
		'images/hour-of-tranquility-couple-4k-gk.jpg',
		'images/night-sky-stars-clouds-scenery-landscape-anime-digital-art-4k-wallpaper-uhdpaper.com-768@0@i.jpg',
		'images/river-forest-scenery-digital-art-4k-wallpaper-uhdpaper.com-907@0@i.jpg',
		'images/scary-house-halloween-night-moon-scenery-digital-art-4k-wallpaper-uhdpaper.com-849@1@m.jpg',
		'images/sunset-anime-comet-stars-scenery-digital-art-4k-wallpaper-uhdpaper.com-771@0@i.jpg',
		'images/sunset-mountain-landscape-scenery-ai-art-4k-wallpaper-uhdpaper.com-744@1@l.jpg',
		'images/the-relaxing-time_1563221945.webp',
		'images/winter-snow-colorful-tree-scenery-digital-art-4k-wallpaper-uhdpaper.com-547@1@n.jpg'
	];
</script>

<script lang="ts">
	import Clock from '$lib/Clock.svelte';

	import './styles.css';
	import { onDestroy, onMount } from 'svelte';

	let image: string | null = $state(null);

	const refreshBackground = () => {
		const index = Math.round(new Date().getTime() / (15 * 60 * 1000)) % images.length;

		image = 'url(' + images[index] + ')';
	};

	const backgroundInterval = setInterval(refreshBackground, 5 * 1000);

	onMount(() => {
		refreshBackground();
	});

	onDestroy(() => {
		clearInterval(backgroundInterval);
	});
</script>

<div class="background" style="background-image:{image}">
	<Clock class="clock" />
</div>

<style>
	.background {
		position: relative;
		height: 100%;
		background-position: center center;
		background-size: cover;
		background-repeat: no-repeat;
		background-color: #000;
	}

	:global(.clock) {
		position: absolute;
		bottom: 2rem;
		right: 1rem;
	}
</style>
