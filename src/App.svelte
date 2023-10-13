<script>
  import Header from "./UI/Header.svelte";
  import Dashboard from "./Pages/Dashboard.svelte";
  import TestPage from "./Pages/TestPage.svelte";
  import Result from "./Pages/Result.svelte";
  import { onMount } from "svelte";
  import ReviewPage from "./Pages/ReviewPage.svelte";

  let page = "start";
  let fetchedData = [];
  let questions = [];
  let totalQuestions = 10;
  let results;
  let reviewNum = 0;

  onMount(async () => {
    let data = await fetch("data/question.json");
    data = await data.json();
    fetchedData = data;
    results = new Array(fetchedData.length);
    let dummy = [];
    fetchedData.forEach((d) => {
      let parseData = JSON.parse(d.content_text);
      d.content_text = parseData;
      dummy.push(parseData);
    });
    questions = dummy;
    totalQuestions = fetchedData.length;
    // console.log(questions);
    // console.log(fetchedData);
  });

  function handleUserInput(e) {
    results[e.detail.questionNumber] = {
      id: e.detail.id,
      is_correct: e.detail.is_correct,
    };
    // console.log(results);
  }

  function handleReview(e) {
    page = "review";
    reviewNum = e.detail;
  }

  function handleDashboard(){
    page="start";
    results=[];
  }
</script>

<Header />

{#if page === "start"}
  <Dashboard on:click on:startTest={() => (page = "test")} />
{:else}
  <main>
    {#if page === "test"}
      <TestPage
        on:endTest={() => (page = "result")}
        on:userInput={handleUserInput}
        {fetchedData}
        {results}
        {questions}
        {totalQuestions}
      />
    {:else if page === "result"}
      <Result
        on:reviewQues={handleReview}
        on:dashboard={handleDashboard}
        {fetchedData}
        {results}
        {questions}
      />
    {:else if page === "review"}
      <ReviewPage on:dashboard={handleDashboard} on:increment={()=>++reviewNum} on:decrement={()=>--reviewNum} on:result={()=>page="result"}  {results} {fetchedData} questionNumber={reviewNum} />
    {/if}
  </main>
{/if}

<style>
</style>
