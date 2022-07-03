<script>
  import { createEventDispatcher } from "svelte";
  import Card from "./Card.svelte";
  export let feedback;

  const dispatch = createEventDispatcher();

  const handleDelete = (id) => dispatch("delete", id);
</script>

<Card>
  <div class="heading">
    <div class="rating">{feedback.rating}</div>
    <i class="material-icons" on:click={() => handleDelete(feedback.id)}
      >delete</i
    >
  </div>
  <div class="review">{feedback.review}</div>
</Card>

<style>
  .rating {
    position: relative;
    background-color: #ffc600;
    padding: 5px;
    left: -1.75rem;
    top: -2rem;
    width: 2rem;
    height: 2rem;
    text-align: center;
    border-radius: 50%;
    /* font-size: 2px; */
    font-weight: bold;
  }
  .heading {
    display: flex;
    justify-content: space-between;
  }
  .review {
    font-style: italic;
    word-wrap: break-word;
  }
  i {
    cursor: pointer;
  }
</style>
