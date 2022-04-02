<script lang="ts">
    import Counter from "./components/Counter.svelte";
</script>

<body>

    <div class="container">
        <h1>Simple Counter</h1>
        <h2>Keep track of things efficiently.</h2>
        <Counter />
    </div>

</body>

<style>
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

</style>