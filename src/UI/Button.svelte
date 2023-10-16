<script>
    export let buttonType = "button";
    export let buttonName = "button";
    export let buttonColor = "primary";
    export let buttonSize = "md";
    export let bgColor = "";
    export let classes = "";
    export let disable = false;
</script>

<button on:click disabled={disable} class="btn bg-{bgColor} {classes} btn-{buttonColor} btn-{buttonSize} text-capitalize" type={buttonType}>
    {buttonName}
</button>

<style>
    button {
        min-width: 100px;
    }
    button:disabled{
        cursor: not-allowed !important;
        pointer-events: all;
    }
  .floating-button{
    position: fixed;
    z-index: 2;
    bottom: 20px;
    right: 30px;
  }
  @media (max-width:850px){
   
    .btn{
      font-size: 80% !important;
      min-width: 20px !important;
    }
  }
</style>