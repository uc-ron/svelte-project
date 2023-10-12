<script>



  import Radio from "../UI/Radio.svelte";
  export let question;
  export let questionNumber;
  export let results = [];
</script>

<p>{question.question}</p>
<div class="d-flex flex-column align-items-start gap-2 w-75">
  {#each question.answers as ans, i (ans.answer)}
    <Radio
      on:userInput
      answereId={ans.id}
      is_correct={ans.is_correct}
      {questionNumber}
      content={ans.answer}
      checked={results[questionNumber]?.id}
      id={i}
    />
  {/each}
</div>

<style>
  p {
    font-size: 1.25em;
  }
</style>
