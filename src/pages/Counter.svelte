<script lang="ts">
    import { onMount } from "svelte";

    import type Dexie from "dexie";

    import type { Counter } from "interfaces/Counter";

    export let db: Dexie;

    // get url param
    const getUrlParam = (name: string) => {
        const url = new URL(window.location.href);
        return url.searchParams.get(name);
    };

    const counterIdParam: string = getUrlParam("c");

    // get counter
    const getCounter = async (id: number) => {
        const counter = await db["counters"].get(id);
        return counter;
    };

    let counter: Counter = {
        count: 0,
    } as Counter;

    onMount(async () => {
        if (counterIdParam) {
            if (isNaN(parseInt(counterIdParam))) {
                // invalid counter id
                return;
            }
            counter = await getCounter(Number(counterIdParam));
        }
    });

    const increment = async () => {
        counter.count++;
        await db["counters"].update(counter.id, counter);
    };

    const decrement = async () => {
        counter.count--;
        await db["counters"].update(counter.id, counter);
    };

    const handleKeyDown = async (e: KeyboardEvent) => {
        if (e.key == " ") {
            await increment();
        }
    }
</script>

<svelte:body on:keydown={handleKeyDown} />

<body>
    <div class="container">
        <h1>{counter.name}</h1>
        <h2>{counter.description}</h2>
        <p class="count">{counter.count}</p>
        <div class="barContainer">
            <div class="barParent">
                <button class="subtractBar" on:click={decrement}>Subtract</button>
                <button class="bar" on:click={increment}>Add</button>
            </div>
        </div>
    </div>
</body>

<style lang="scss">
    :global(body) {
        background-color: #171717;
    }

    body {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .container {
        display: flex;
        flex-direction: column;
        color: white;
        text-align: center;
    }

    .count {
        font-size: 4rem;
        font-weight: bold;
    }

    .barContainer {
        width: 100%;

        display: flex;
        justify-content: center;
    }

    .barParent {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;

        @media only screen and (max-width: 800px) {
            width: 90%;
        }
    }

    .bar {
        height: 5rem;
        width: 60%;
        display: flex;
        text-align: center;
        border-radius: 5px;
        color: black;
        border: 1px solid white;
        background-color: transparent;

        display: flex;
        justify-content: center;
        align-items: center;

        cursor: pointer;

        transition-duration: 512ms;

        &:hover {
            background-color: rgb(124, 255, 124);
        }

        &:active {
            background-color: rgb(76, 255, 76);
        }

        background-color: rgb(183, 255, 183);
    }

    .subtractBar {
        @extend .bar;

        width: 38%;

        background-color: rgb(255, 183, 183);

        &:hover {
            background-color: rgb(255, 148, 148);
        }

        &:active {
            background-color: rgb(255, 84, 84);
        }
    }
</style>
