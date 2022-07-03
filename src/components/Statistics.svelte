<script>
  export let feedbacks = [];

  $: count = feedbacks.length;
  $: average =
    feedbacks.reduce(
      (previousValue, current) => previousValue + current.rating,
      0
    ) / count;
</script>

<div class="container">
  {#if count}
    <div>{count} reviews</div>
    <div>Average: {average.toFixed(1)}</div>
  {:else}
    <div>No review yet.</div>
  {/if}
</div>

<style>
  .container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    color: white;
    font-weight: bold;
  }
</style>
