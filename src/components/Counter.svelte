<script lang="ts">
    import type Dexie from "dexie";

    import { afterUpdate } from "svelte";

    export let name: string = "Unnamed Counter";
    export let description: string = "No description yet.";
    export let color: string = "#ffffff";
    export let id: number = 0;
    export let db: Dexie;

    let nameChanged: boolean = false;

    let showEditor: boolean = false;

    const doRename = async () => {
        if (!nameChanged) {
            showEditor = false;
            return;
        }

        const counter = {
            name: name,
            description: description,
            color: color,
            id: id,
        };
        await db["counters"].put(counter);
        showEditor = false;
    };

    let input: HTMLInputElement;

    afterUpdate(() => {
        if (showEditor) {
            input.focus();
        }
    });
</script>

<body>
    <div class="container">
        <div class="colorParent">
            <div class="color" style={`background: ${color}`} />
        </div>
        <div class="info">
            <!-- make title an editable name component -->
            {#if showEditor}
                <input
                    class="editor"
                    type="text"
                    bind:value={name}
                    bind:this={input}
                    on:keypress={(e) => {
                        if (e.key === "Enter") {
                            doRename();
                        } else {
                            if (!nameChanged) {
                                nameChanged = true;
                            }
                        }
                    }}
                />
            {:else}
                <p
                    class="title"
                    on:click={() => {
                        showEditor = true;
                    }}
                >
                    {name}
                </p>
            {/if}
            <p class="description">
                {description}
            </p>
        </div>
    </div>
</body>

<style lang="scss">
    .container {
        width: 20rem;
        border-radius: 10px;
        border: 1px solid white;
        color: white;
        height: 5rem;
        padding: 1rem;
        display: flex;
        align-items: center;

        transition-duration: 512ms;

        &:hover {
            cursor: pointer;
        }

        margin: 1rem 0 1rem 0;
    }

    .colorParent {
        width: 40%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .color {
        width: 5rem;
        height: 5rem;
        border-radius: 10px;

        border: 1px solid black;

        transition-duration: 512ms;

        &:hover {
            box-shadow: 0 5px 10px 1px rgb(77, 77, 77);
        }
    }

    .info {
        width: 100%;
        padding-left: 1rem;
        height: 100%;
        display: flex;
        flex-direction: column;
    }

    .title {
        font-weight: bold;
        font-size: 1.5rem;
        text-align: left;
        margin: 0;

        border-bottom: 1px solid transparent;
        margin-bottom: 0.5rem;

        &:hover {
            border-bottom: 1px solid white;
        }
    }

    .editor {
        @extend .title;

        background-color: transparent;
        color: white;
        width: 100%;
        font-size: 1rem;
    }

    .description {
        margin: 0;
        text-align: left;
    }
</style>
