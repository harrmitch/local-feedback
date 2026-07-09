<script>
  /**
   * @typedef {Object} Props
   * @property {import('svelte').Snippet} [children]
   */

  /** @type {Props} */
  let { children } = $props();
</script>

<div class="card">
  {@render children?.()}
</div>

<style>
  .card {
    background-color: white;
    margin: 2rem 0;
    padding: 1rem;
    border-radius: 0.5rem;
  }
</style>
