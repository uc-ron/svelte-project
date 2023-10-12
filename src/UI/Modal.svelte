<script>
  import { createEventDispatcher } from "svelte";
  import Button from "./Button.svelte";

  export let message;
  export let results;
  let unattempted = results.length;
  for (let i = 0; i < results.length; i++) {
    if (results[i]) {
      --unattempted;
    }
  }
  const dispatch = createEventDispatcher();
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div
  on:click={() => dispatch("cancel")}
  class="position-absolute top-0 z-1 w-100 h-100 backdrop d-flex justify-content-center align-items-center"
>
  <div class="w-50 h-auto rounded bg-light d-flex flex-column container p-2">
    <div class="d-flex align-items-center justify-content-between">
      <h3>Confirmation</h3>
      <button on:click={() => dispatch("cancel")} class="btn fw-bold">X</button>
    </div>
    <p class="text-center lead p-2 font-lg">
      {message}
    </p>
    <div class="d-flex justify-content-around align-items-center pb-5">
      <div class="d-flex flex-column text-primary badge p-3 border border-primary">
        <h1 class="m-0 text-center fw-bold">{results.length}</h1>
        <p class="m-0">Items</p>
      </div>
      <div class="d-flex flex-column text-success badge p-3 border border-success">
        <h1 class="m-0 text-center fw-bold">{results.length - unattempted}</h1>
        <p class="m-0">Attempted</p>
      </div>
      <div class="d-flex flex-column text-warning badge p-3 border border-warning">
        <h1 class="m-0 text-center fw-bold">{unattempted}</h1>
        <p class="m-0 ">Unattempted</p>
      </div>
    </div>
    <div class="d-flex justify-content-end gap-4">
      <Button
        on:click={() => dispatch("cancel")}
        buttonName="cancel"
        buttonColor="secondary"
      />
      <Button
        on:click={() => dispatch("goToList")}
        buttonName="go to items list"
        buttonColor="primary"
      />
      <Button
        on:click={() => dispatch("endTest")}
        buttonName="end test"
        buttonColor="danger"
      />
    </div>
  </div>
</div>

<style>
  .backdrop {
    background: rgba(0, 0, 0, 0.8);
  }
  p {
    font-weight: 400;
  }
</style>
