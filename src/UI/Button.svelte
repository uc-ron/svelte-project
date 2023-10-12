<script>
    export let buttonType = "button";
    export let buttonName = "button";
    export let buttonColor = "primary";
    export let buttonSize = "md";
    export let bgColor = "";
    export let disable = false;
</script>

<button on:click disabled={disable} class="btn bg-{bgColor} btn-{buttonColor} btn-{buttonSize} text-capitalize" type={buttonType}>
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
</style>