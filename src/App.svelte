<script lang="ts">
    import Counter from "./components/Counter.svelte";
</script>

<body>

    <div class="container">
        <h1>Simple Counter</h1>
        <h2>Keep track of things efficiently.</h2>
        <button class="add">Create Counter</button>
        <Counter />
    </div>

</body>

<style lang="scss">
    :global(body) {
        padding: 0;
        margin: 0;
    }

    body {
        background: #171717;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .container {
        color: white;
        text-align: center;
    }

    h2 {
        font-weight: normal;
    }

    .add {
        width: 100%;
        border-radius: 10px;
        border: 1px solid white;
        color: white;
        height: 3rem;

        background: transparent;
        text-align: center;

        transition-duration: 512ms;

        &:hover {
            cursor: pointer;
            background-color: white;
            color: black;
            transform: translateY(-6px);
        }
    }

</style>