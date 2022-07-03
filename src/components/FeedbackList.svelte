<script>
  import { flip } from "svelte/animate";
  import { fade, scale } from "svelte/transition";
  import FeedbackItem from "./FeedbackItem.svelte";

  export let feedbacks = [];

  const deleteFeedback = (id) => {
    feedbacks = feedbacks.filter((feedback) => feedback.id != id);
  };
</script>

<div class="container">
  {#each feedbacks as feedback (feedback.id)}
    <div
      in:scale={{ delay: 500 }}
      out:fade={{ duration: 300 }}
      animate:flip={{ delay: 200 }}
    >
      <FeedbackItem {feedback} on:delete={(e) => deleteFeedback(e.detail)} />
    </div>
  {/each}
</div>
