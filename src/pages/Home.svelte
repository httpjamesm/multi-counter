<script lang="ts">
    import Counter from "../components/Counter.svelte";
    import { onMount } from "svelte";

    import type Dexie from "dexie";

    export let db: Dexie;

    const getCounters = async () => {
        const allCounters = await db["counters"].toArray();
        return allCounters;
    };

    let counters = [];

    const getCountersFromChild = async () => {
        counters = await getCounters();
    };

    // on mount
    onMount(async () => {
        counters = await getCounters();
    });

    const createCounter = async () => {
        const counter = {
            name: "Unnamed Counter",
            description: "No description yet.",
            color: "#ffffff",
            count: 0,
        };
        await db["counters"].add(counter);
        counters = await getCounters();
    };
</script>

<body>
    <div class="container">
        <h1>Multi Counter</h1>
        <h2>Keep track of things efficiently.</h2>
        <button class="add" on:click={createCounter}>Create Counter</button>
        {#each counters as counter (counter.id)}
            <Counter
                {db}
                id={counter.id}
                name={counter.name}
                description={counter.description}
                color={counter.color}
                getCounters={getCountersFromChild}
            />
        {/each}
        <p>
            Made with love by <a
                href="https://httpjames.space"
                target="_blank"
                rel="noopener noreferrer"
            >
                http.james</a
            >
            in
            <a
                href="https://svelte.dev"
                target="_blank"
                rel="noopener noreferrer">Svelte</a
            >.
        </p>
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

    h2 {
        margin-bottom: 1rem;
    }
</style>
