<script>
  import { beforeUpdate, createEventDispatcher, onMount } from "svelte";

  const dispatch = createEventDispatcher();

  export let data = [];
  export let questionNumber;
  export let results;
  let filter = "all";
  let unattempted = [];
  let attempted = [];
  let newData;
  onMount(() => {
    let temp = [];
    data.forEach((e) => {
      temp.push({ ...e, attempted: false, id: temp.length });
    });
    data = temp;
    newData = data;
  });

  beforeUpdate(() => {
    attempted = [];
    unattempted = [];
    for (let i = 0; i < results.length; i++) {
      if (results[i]?.id) {
        attempted.push({ ...data[i], attempted: true });
      } else {
        unattempted.push({ ...data[i], attempted: false });
      }
    }
    if (filter === "attempted") {
      newData = attempted;
    } else if (filter === "unattempted") {
      newData = unattempted;
    } else {
      newData = data;
    }
  });
</script>

<div
  class="sidebar w-700px position-absolute z-1 overflow-y-scroll bg-lightblue"
>
  <div class="p-2 d-flex flex-column">
    <ul class="btn-group">
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <li
        on:click={() => (filter = "all")}
        class="btn {`${
          filter === 'all' ? 'bg-primary btn-primary' : 'bg-gray'
        }`}"
      >
        All
      </li>
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <li
        class="btn bg-gray {`${
          filter === 'attempted' ? 'bg-primary btn-primary' : 'bg-gray'
        }`}"
        on:click={() => (filter = "attempted")}
      >
        Attempted
      </li>
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <li
        on:click={() => (filter = "unattempted")}
        class="btn bg-gray {`${
          filter === 'unattempted' ? 'bg-primary btn-primary' : 'bg-gray'
        }`}"
      >
        Unattempted
      </li>
    </ul>
    <ul class="d-flex flex-column gap-2 align-items-start p-0">
      {#each newData as ques, i (ques.content_id)}
        <button on:click={() => dispatch("jumpTo", ques.id)}>
          <li class="d-flex gap-3 align-items-center btn">
            <div class="float-start btn-sm btn-secondary rounded-circle">
              {ques.id+1}
            </div>
            <div class="d-flex flex-column gap-1 align-items-start">
              <p
                class="{`${
                  questionNumber === ques.id ? 'text-primary' : 'text-secondary'
                }`}  m-0 text-start fw-bold"
              >
                {ques.snippet}[061bF]
              </p>
              {#if ques.attempted ||( results[i]?.id && filter ==="all")}
                <span
                  class="rounded-pill btn btn-sm small text-success border-success"
                >
                  Attempted
                </span>
              {:else}
                <span
                  class="rounded-pill btn btn-sm small text-warning border-warning"
                >
                  Unattempted
                </span>
              {/if}
            </div>
          </li>
        </button>
      {/each}
    </ul>
  </div>
</div>

<style>
  * {
    font-weight: 400;
    font-size: 90%;
  }
  li:hover {
    background: #ebebeb;
  }
  button {
    border: none;
    background: none;
  }
  .sidebar {
    top: 4rem;
    margin: 0;
    padding: 0;
    height: calc(100% - 9rem);
  }

  .sidebar::-webkit-scrollbar {
    width: 8px;
    /* Set the width of the scrollbar */
  }

  /* Thumb styles for the scrollbar */
  .sidebar::-webkit-scrollbar-thumb {
    background-color: #333;
    /* Set the color of the scrollbar thumb */
    border-radius: 4px;
    /* Add some rounded corners to the thumb */
  }

  /* Handle styles for the scrollbar (only for Webkit browsers) */
  .sidebar::-webkit-scrollbar-thumb:hover {
    background-color: #555;
    /* Change the thumb color on hover */
  }

  /* Track styles for the scrollbar (only for Webkit browsers) */
  .sidebar::-webkit-scrollbar-track {
    background-color: #ccc;
    /* Set the color of the scrollbar track */
  }
  span {
    font-size: 70%;
  }
</style>
