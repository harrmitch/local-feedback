<script>
  import uniqid from "uniqid";
  import Card from "./Card.svelte";
  let { feedbacks = $bindable() } = $props();

  const VALUES = [...Array(11).keys()].splice(1);
  const MIN_CHAR_COUNT = 50;

  let text = $state("");
  let message = $state();
  let invalid = $derived(text.replace(/\s/g, " ").length < MIN_CHAR_COUNT);
  let selected = $state(10);

  const submitHandler = () => {
    if (invalid) {
      message = `Please submit at least ${MIN_CHAR_COUNT} characters.`;
    } else {
      let newFeedback = { id: uniqid(), rating: selected, review: text };
      feedbacks = [newFeedback, ...feedbacks];

      text = "";
      selected = 10;
      message = null;
    }
  };
</script>

<Card>
  <div class="container">
    <header><h1>How do you feel about our service?</h1></header>

    <div class="rating-form">
      {#each VALUES as value}
        <input
          type="radio"
          bind:group={selected}
          name="rating"
          {value}
          id={value.toString()}
        />
        <label for={value.toString()}>
          {value}
        </label>
      {/each}
    </div>

    <form onsubmit={(e) => {
      e.preventDefault();
      submitHandler();
    }}>
      <input
        type="text"
        bind:value={text}
        placeholder={`Write at least ${MIN_CHAR_COUNT} characters to submit.`}
      />
      <button class={invalid ? "disabled" : ""}>Send</button>
    </form>

    {#if message}
      <p class="warning">{message}</p>
    {/if}
  </div>
</Card>

<style>
  .container {
    padding: 1rem 0;
  }
  header {
    text-align: center;
  }
  form {
    display: flex;
    justify-content: center;
    margin: 0 2rem;
    height: 2rem;
  }
  [type="text"] {
    width: 90%;
  }
  button {
    width: 10%;
    background-color: #ffc600;
    font-weight: bold;
  }
  button:hover {
    width: 10%;
    background-color: #ffc600;
    font-weight: bold;
    opacity: 80%;
  }
  button.disabled {
    width: 10%;
    background-color: grey;
    font-weight: bold;
    opacity: 80%;
  }
  .warning {
    color: red;
    text-align: center;
  }
  .rating-form {
    display: flex;
    align-content: center;
    justify-content: space-around;
    width: 80%;
    margin: 1rem auto;
  }
  [type="radio"] {
    opacity: 0;
    position: fixed;
    width: 0;
  }
  label {
    background-color: grey;
    text-align: center;
    padding: 5px;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
  }
  [type="radio"]:checked + label {
    background-color: #ffc600;
    text-align: center;
    padding: 5px;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    border: 2px solid black;
    font-weight: bold;
  }
  label:hover {
    background-color: #ffc600;
    text-align: center;
    padding: 5px;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    border: 2px solid black;
    font-weight: bold;
    opacity: 70%;
  }
  /* [type="radio"]:focus + label {
    background-color: #ffc600;
    text-align: center;
    padding: 5px;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    border: 2px dashed black;
    font-weight: bold;
  } */
</style>
