<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../UI/Button.svelte";

  const dispatch = createEventDispatcher();

  export let fetchedData;
  export let results;
  let unattempted = fetchedData.length;
  let correct = 0;
  let incorrect;
  let item = results?.length;
  let resultInPercentage;
  for (let i = 0; i < fetchedData.length; i++) {
    if (results[i]) {
      --unattempted;
    }
    if (results[i]?.is_correct == "1") {
      correct++;
    }
  }
  resultInPercentage = Math.round((correct / item) * 100);
  incorrect = item - unattempted - correct;
</script>

<div class="main">
  <div class="container">
    <div class="d-flex align-items-center flex-column gap-3">
      <h2 class="m-0">Test Name</h2>
      <span class="underline" />
      <p class="text-uppercase">
        <span class="fw-bold text-danger">TEST MODE</span> ON, 11-OCT-23, 09:15
        am ist,
        <span class="fw-bold text-success">time taken</span>: 44m
      </p>
      <div class="d-flex gap-1">
        <div
          class="btn bg-lightgray border-primary d-flex align-items-center flex-column px-5"
        >
          <div class="text-info">{resultInPercentage}%</div>
          <div class="text-dark">Result</div>
        </div>
        <div
          class="btn bg-lightgray border-primary d-flex align-items-center flex-column px-4"
        >
          <div class="text-primary">{item}</div>
          <div class="text-dark">Items</div>
        </div>
        <div
          class="btn bg-lightgray border-primary d-flex align-items-center flex-column px-4"
        >
          <div class="text-success">{correct}</div>
          <div class="text-dark">Correct</div>
        </div>
        <div
          class="btn bg-lightgray border-primary d-flex align-items-center flex-column px-4"
        >
          <div class="text-danger">
            {incorrect}
          </div>
          <div class="text-dark">Incorrect</div>
        </div>
        <div
          class="btn bg-lightgray border-primary d-flex align-items-center flex-column px-4"
        >
          <div class="text-warning">{unattempted}</div>
          <div class="text-dark">Unattempted</div>
        </div>
      </div>
    </div>
    <div class="d-flex justify-content-between pt-3">
      <Button buttonColor="light" bgColor="gray" buttonName="Review" />
      <input type="text" placeholder="Search" />
    </div>
    <div class="w-100 rounded py-4">
      <ul
        class="d-flex flex-column justify-content-between p-0 align-items-start table-striped"
      >
        {#each fetchedData as ques, i (ques.content_id)}
          <li
            class="d-flex gap-3 align-items-center justify-content-between p-2 border-bottom w-100"
          >
            <div class="d-flex gap-3 align-items-center w-75">
              <div class="float-start btn-sm btn-secondary rounded-circle">
                {i + 1}
              </div>
              <div class="d-flex flex-column gap-1 align-items-start">
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <p
                  class=" m-0 text-start btn item"
                  on:click={() => dispatch("reviewQues", i)}
                >
                  {ques.snippet} .[061bF]
                </p>
              </div>
            </div>
            <div class="d-flex justify-content-between w-25">
              <div class="btn-group gap-1 text-uppercase w-50">
                {#each ques.content_text.answers as ans, index (ans.id)}
                  <span
                    class="rounded px-1 border text-secondary {`${
                      results[i]?.id == ans.id ? 'bg-danger text-light ' : ''
                    }`} {`${
                      ans.is_correct === '1' ? 'bg-success text-light ' : ''
                    }`}"
                  >
                    {String.fromCharCode(65 + index)}
                  </span>
                {/each}
                <!-- <div px-1ounded border fw-bold text-secondary">b</div>
                  <div class="p-1 rounded border fw-bold text-secondary">c</div>
                  <div class="p-1 rounded border fw-bold text-secondary">d</div> -->
              </div>
              <div class="w-50 text-center">
                {#if results[i]}
                  {#if results[i].is_correct === "1"}
                    <span class="text-success badge border border-success"
                      >Correct</span
                    >
                  {:else}
                    <span class="text-danger badge border border-danger"
                      >Incorrect</span
                    >
                  {/if}
                {:else}
                  <span class="text-warning badge border border-warning"
                    >Unattempted</span
                  >
                {/if}
              </div>
            </div>
          </li>
        {/each}
      </ul>
    </div>
  </div>
</div>

<style>
  .main {
    padding-top: 5rem;
    height: calc(100vh - 5rem);
  }
  .item:hover {
    color: red;
  }
  .bg-success {
    background: #198754 !important;
  }
  .underline {
    height: 1px;
    width: 20vw;
    background: #000;
  }
  input {
    width: 25%;
    padding: 0 1rem;
    border-radius: 10px;
    border: 1px solid #ccc;
  }
  .table-striped > :nth-child(even) {
    background: #f1f1f1;
  }
  .table-striped {
    border-top: 3px solid #96bbf6;
  }
  p {
    font-size: 90%;
  }
</style>
