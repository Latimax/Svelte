<script>
    export let type = "primary"; // Default type is button
    export let flat = false; // Default flat is false
    export let inverse = false;
</script>

<button class={type} class:flat={flat} class:inverse={inverse}>
    <slot></slot>
</button>


<style>
    button{
        border: 0;
        cursor: pointer;
        border-radius: 6px;
        padding: 8px 12px;
        font-weight: bold;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
    }

    .primary {
        background: #d91b42;
        color: white;
    }

    .secondary {
        background: #45c496;
        color: white;
    }

    .flat{
        box-shadow: none;
    }

    .primary.inverse{
        background: white;
        color: #d91b42;
        border: 2px solid #d91b42;
    }

    .secondary.inverse{
        background: white;
        color: #45c496;
        border: 2px solid #45c496;
    }
</style>