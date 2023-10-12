<script>
  import { afterUpdate, beforeUpdate, createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let questionNumber;
  export let content = "radio";
  export let answereId;
  export let checked;
  export let is_correct;
  export let disabled = false;

  export let id;
</script>

{#if disabled && checked === answereId && is_correct != "1"}
  <div class="d-flex gap-2 bg-danger text-white w-75">
    <input
      on:click={() =>
        dispatch("userInput", {
          id: answereId,
          questionNumber,
          is_correct: is_correct,
        })}
      type="radio"
      class="form-check-input"
      name="option"
      {disabled}
      {id}
      checked={checked === answereId}
    />
    <label for={id}>{content}</label>
  </div>
{:else if disabled && is_correct == "1"}
  <div class="d-flex gap-2 bg-success text-white w-75">
    <input
      on:click={() =>
        dispatch("userInput", {
          id: answereId,
          questionNumber,
          is_correct: is_correct,
        })}
      type="radio"
      class="form-check-input"
      name="option"
      {disabled}
      {id}
      checked={checked === answereId}
    />
    <label for={id}>{content}</label>
  </div>
{:else}
  <div class="d-flex gap-2">
    <input
      on:click={() =>
        dispatch("userInput", {
          id: answereId,
          questionNumber,
          is_correct: is_correct,
        })}
      type="radio"
      class="form-check-input"
      name="option"
      {disabled}
      {id}
      checked={checked === answereId}
    />
    <label for={id}>{content}</label>
  </div>
{/if}

<style>
  input{
    min-height: 15px;
    min-width: 15px;
  }
</style>
