<script>
  import Question from "../UI/Question.svelte";
  import Footer from "../UI/Footer.svelte";
  import Sidebar from "../UI/Sidebar.svelte";
  import Modal from "../UI/Modal.svelte";

  let questionNumber = 0;
  export let totalQuestions = 10;
  export let fetchedData = [];
  export let questions = [];
  export let results = [];
  let sidebar = false;
  let modal = false;
  let message;

  // $: sidebar = isNaN(questionNumber);

  function handleJumpTo(e) {
    questionNumber = e.detail;
    sidebar = false;
  }
  function handleModal(e) {
    message = e.detail;
    sidebar=false;
    modal = true;
  }
  function handleIncrement() {
    ++questionNumber;
    sidebar = false;
  }
  function handleDecrement() {
    --questionNumber;
    sidebar = false;
  }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<section on:click={() => (sidebar = false)} class="main">
  <div class="container">
    <Question
      on:userInput
      {results}
      {questionNumber}
      fetchedData={fetchedData[questionNumber]}
      question={questions[questionNumber]}
    />
  </div>
</section>
{#if modal}
  <Modal
    on:goToList={() => (sidebar = true)}
    on:cancel={() => (modal = false)}
    on:endTest
    {results}
    {message}
    {totalQuestions}
  />
{/if}
{#if sidebar}
  <Sidebar
    {results}
    {questionNumber}
    on:jumpTo={handleJumpTo}
    data={fetchedData}
  />
{/if}
<Footer
  on:endTest
  on:increment={handleIncrement}
  on:decrement={handleDecrement}
  {questionNumber}
  {totalQuestions}
  on:toggleList={() => (sidebar = !sidebar)}
  on:openModal={handleModal}
/>

<style>
  .main {
    padding-top: 5rem;
    height: calc(100vh - 5rem);
  }
</style>
