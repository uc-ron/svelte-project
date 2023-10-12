<script>
  import Button from "../UI/Button.svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
</script>

<main class="h-100 d-flex justify-content-center align-items-center">
  <Button
    on:click={() => dispatch("startTest")}
    buttonName="start test"
    buttonSize="lg"
  />
</main>

<style>
</style>
