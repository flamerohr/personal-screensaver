<script lang="ts">
  import { format } from 'date-fns';

  let { class: className = '' } = $props();

  let now = $state(new Date());
  let time = $derived(format(now, 'h:mm aaa'));
  let date = $derived(format(now, 'ccc, d MMM'));

  $effect(() => {
    const interval = setInterval(() => (now = new Date()), 15 * 1000);

    return () => clearInterval(interval);
  });
</script>

<div class="{className} clock">
  <div class="time">{time}</div>
  <div class="date">{date}</div>
</div>

<style>
  .clock {
    --size: 42pt;
    --size: max(min(15vh, 7.5vw, 200pt), 42pt);
    font-size: var(--size);
    color: #ccc;

    background: rgb(0, 0, 0, 0.2);
    background: radial-gradient(circle, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.3) 100%);
    border-radius: calc(var(--size) / 2);
    padding: calc(var(--size) / 10) calc(var(--size) / 5);

    text-align: end;
  }
  .date {
    font-size: calc(var(--size) / 2);
  }
</style>
