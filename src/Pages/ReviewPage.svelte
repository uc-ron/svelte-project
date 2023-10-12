<script>
  import { afterUpdate, beforeUpdate } from "svelte";
  import ReviewFooter from "../UI/ReviewFooter.svelte";
  import ReviewQuestion from "../UI/ReviewQuestion.svelte";

  export let fetchedData;
  export let questionNumber = 0;
  export let results;
  export let status;
</script>

<section class="main">
  <div class="container">
    <ReviewQuestion
      {status}
      question={fetchedData[questionNumber].content_text}
      {questionNumber}
      {results}
    />
  </div>
</section>
<ReviewFooter
  on:dashboard
  on:increment
  on:decrement
  on:result
  {questionNumber}
  totalQuestions={fetchedData.length}
/>

<style>
  .main {
    padding-top: 5rem;
    height: calc(100vh - 5rem);
    overflow-y: scroll;
  }
</style>
