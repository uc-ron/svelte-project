<script>
  import { beforeUpdate } from "svelte";
  import Radio from "./Radio.svelte";

  export let question;
  export let questionNumber;
  export let results;
  export let status = "unattempted";

  beforeUpdate(() => {
    if (results[questionNumber]?.id) {
      let index;
      for (let i = 0; i < 4; i++) {
        if (question.answers[i].id == results[questionNumber].id) {
          index = i;
        }
      }
      if (question.answers[index].is_correct === "1") {
        status = "Correct";
      } else {
        status = "Incorrect";
      }
    } else {
      status = "Incorrect";
    }
  });
</script>

<div class="container p-2 text-center mb-2">
  {#if status === "Correct"}
    <span class="rounded p-2 bg-success text-white"> {status} </span>
  {:else}
    <span class="rounded p-2 bg-danger text-white"> {status} </span>
  {/if}
</div>
<p>{question.question}</p>
<div class="d-flex flex-column align-items-start gap-2 w-75">
  <!-- <label for="1"></label> -->
  {#each question.answers as ans, i (ans.id)}
    <Radio
      content={ans.answer}
      answereId={ans.id}
      id={i}
      is_correct={ans.is_correct}
      checked={results[questionNumber]?.id}
      disabled={true}
      {questionNumber}
    />
  {/each}
</div>
<hr>
<p>{question.explanation}</p>
