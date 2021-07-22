<script>
  import Question from './Question.svelte';

  let currentQuestion = getQuestion();

  async function getQuestion() {
    const res = await fetch(
      'https://opentdb.com/api.php?amount=1&type=multiple'
    );
    return await res.json();
  }

  function handleClick() {
    currentQuestion = getQuestion();
  }
</script>

<div>
  <button on:click={handleClick}>Get Question</button>
</div>

{#await currentQuestion}
  Loading...
{:then data}
  <Question question={data.results[0]} />
{/await}

<style>
</style>
