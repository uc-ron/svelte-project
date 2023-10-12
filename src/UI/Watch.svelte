<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let timeInMin = 90;
  let timer = timeInMin * 60;
  let testEnded = false;
  let hours = Math.floor(timer / 3600);
  let minutes = Math.floor((timer % 3600) / 60);
  let seconds = timer % 60;
  hours = hours < 10 ? "0" + hours : hours;
  minutes = minutes < 10 ? "0" + minutes : minutes;
  seconds = seconds < 10 ? "0" + seconds : seconds;

  function updateTime() {
    if (timer > 0) {
      timer--;
      hours = Math.floor(timer / 3600);
      minutes = Math.floor((timer % 3600) / 60);
      seconds = timer % 60;

      // Add leading zeros to single-digit hours, minutes, and seconds
      hours = hours < 10 ? "0" + hours : hours;
      minutes = minutes < 10 ? "0" + minutes : minutes;
      seconds = seconds < 10 ? "0" + seconds : seconds;
    } else {
      clearInterval(interval); // Stop the interval when the timer reaches 0
      setTimeout(() => {
        dispatch("endTest");
      }, 3000);
      testEnded = true;
    }
  }

  const interval = setInterval(updateTime, 1000);
</script>

{#if testEnded}
  <div
    class="position-absolute top-0 z-1 w-50 h-100 backdrop d-flex justify-content-center align-items-center"
  >
    <div
      class="w-50 h-auto rounded text-light d-flex flex-column container p-2"
    >
      Time Over...
    </div>
  </div>
{/if}
<span>{hours + ":" + minutes + ":" + seconds}</span>

<style>
  .backdrop {
    background: rgba(0, 0, 0, 0.8);
  }
</style>
