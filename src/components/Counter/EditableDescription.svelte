<script lang="ts">
    import type Dexie from "dexie";

    import { afterUpdate } from "svelte";

    export let db: Dexie;

    export let description: string;

    export let id: number;

    let descChanged: boolean = false;

    let input: HTMLTextAreaElement;

    let showEditor: boolean = false;

    const doEdit = async () => {
        if (!descChanged) {
            showEditor = false;
            return;
        }

        await db["counters"].update(id, {
            description,
        });
        showEditor = false;
    };

    afterUpdate(() => {
        if (showEditor) {
            input.focus();
        }
    });

</script>

{#if showEditor}
    <textarea
        class="editor"
        type="text"
        bind:this={input}
        bind:value={description}
        on:keypress={(e) => {
            if (e.key === "Enter") {
                doEdit();
            } else {
                if (!descChanged) {
                    descChanged = true;
                }
            }
        }}
    />
{:else}
    <p
        class="description"
        on:click={() => {
            showEditor = true;
        }}
    >
        {description}
    </p>
{/if}

<style lang="scss">
    .description {
        margin: 0;
        text-align: left;
    }

    .editor {
        @extend .description;

        background-color: transparent;
        color: white;
        width: 100%;
        font-size: 1rem;

        border: none;
        border-bottom: 1px solid white;

        border-radius: 10px;

        &:focus {
            outline: none;
        }

        &:hover {
            border-bottom: 1px solid white;
        }

        resize: none;
    }

</style>