<script>
  import Button from "./Button.svelte";
  import { createEventDispatcher } from "svelte";
  import Watch from "./Watch.svelte";

  export let questionNumber = 1;
  export let totalQuestions = 10;

  const dispatch = createEventDispatcher();

  function handleIncrement() {
    if (questionNumber !== totalQuestions-1) {
      dispatch("increment");
    } else {
      dispatch(
        "openModal",
        "You are on the last item. Review your items list or End your test."
      );
    }
  }
</script>

<footer class="shadow-lg">
  <div
    class="w-100 h-100 d-flex align-items-center justify-content-end p-1 px-5 gap-3"
  >
    <Watch on:endTest />
    <Button
      on:click={() => dispatch("toggleList")}
      buttonName="list"
      buttonColor="secondary"
    />
    <Button
      on:click={() => dispatch("decrement")}
      disable={questionNumber > 0 ? false : true}
      buttonName="previous"
      buttonColor="secondary"
    />
    <span class="btn">{questionNumber + 1} of {totalQuestions}</span>
    <Button
      on:click={handleIncrement}
      buttonName="next"
      buttonColor="secondary"
    />
    <Button
      on:click={() =>
        dispatch(
          "openModal",
          "This action will end your test. Do you want to proceed?"
        )}
      buttonName="end test"
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
