<script lang="ts">
	import { onDestroy } from 'svelte';
	import { format } from 'date-fns';

	let { class: className = '' } = $props();

	let now = new Date();
	let time = $derived(format(now, 'h:mm aaa'));
	let date = $derived(format(now, 'ccc, do MMM'));

	const interval = setInterval(() => (now = new Date()), 15 * 1000);

	onDestroy(() => {
		clearInterval(interval);
	});
</script>

<div class="{className} clock">
	<div class="time">{time}</div>
	<div class="date">{date}</div>
</div>

<style>
	.clock {
    --size: 42px;
    --size: min(20vh, 10vw);
		font-size: var(--size);
		color: #ccc;

    background: rgb(0,0,0, 0.2);
    background: radial-gradient(circle, rgba(0,0,0,0.5) 0%, rgba(0,0,0,0.3) 100%);
    border-radius: calc(var(--size) / 2);
    padding: calc(var(--size) / 10) calc(var(--size) / 5);
	}
  .date {
		font-size: calc(var(--size) / 2);
  }
</style>
