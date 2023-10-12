<script>
  import { createEventDispatcher } from "svelte";
  import Button from "./Button.svelte";

  const dispatch = createEventDispatcher();

  export let questionNumber;
  export let totalQuestions;
</script>

<footer class="shadow-lg">
  <div
    class="w-100 h-100 d-flex align-items-center justify-content-end p-1 px-5 gap-3 bg-white"
  >
    <Button on:click={()=>dispatch("dashboard")} buttonName="Dashboard" buttonColor="secondary" />
    <Button
      on:click={() => dispatch("decrement")}
      disable={questionNumber > 0 ? false : true}
      buttonName="previous"
      buttonColor="secondary"
      />
      <span class="btn">{questionNumber + 1} of {totalQuestions}</span>
      <Button
      on:click={() => dispatch("increment")}
      buttonName="next"
      buttonColor="secondary"
      disable={questionNumber < totalQuestions ? false : true}
      />
    <Button
      on:click={() => dispatch("result")}
      buttonName="Result"
      buttonColor="secondary"
    />
  </div>
</footer>

<style>
  footer {
    position: absolute;
    height: 5rem;
    width: 100%;
    bottom: 0;
    border-top: 2px solid #ccc;
  }
</style>
