<script>
  export let question;

  let isCorrect;
  let answers = question.incorrect_answers.map((answer) => {
    return {
      answer,
      correct: false,
    };
  });
  let allAnswers = [
    ...answers,
    {
      answer: question.correct_answer,
      correct: true,
    },
  ];

  shuffle(allAnswers);

  function shuffle(array) {
    array.sort(() => Math.random() - 0.5);
  }
  function checkAnswer(correct) {
    if (correct) {
      isCorrect = true;
    }
  }
</script>

<h1>{@html question.question}</h1>

{#each allAnswers as answer}
  <button
    style="color: {answer.correct ? 'green' : 'red'}"
    on:click={() => checkAnswer(answer.correct)}>{@html answer.answer}</button
  >
{/each}
{#if isCorrect}
  <h2>Correct!</h2>
{/if}
