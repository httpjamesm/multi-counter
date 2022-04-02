<script lang="ts">
    import type Dexie from "dexie";

    import { afterUpdate } from "svelte";

    export let db: Dexie;

    export let id: number;

    export let name: string;

    let nameChanged: boolean = false;

    let input: HTMLInputElement;

    let showEditor: boolean = false;

    const doRename = async () => {
        if (!nameChanged) {
            showEditor = false;
            return;
        }

        await db["counters"].update(id, {
            name,
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
    <input
        class="editor"
        type="text"
        bind:this={input}
        bind:value={name}
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

<style lang="scss">
    .title {
        font-weight: bold;
        font-size: 1.5rem;
        text-align: left;
        margin: 0;

        border-bottom: 1px solid transparent;
        margin-bottom: 0.5rem;

        &:hover {
            border-bottom: 1px solid rgb(55, 55, 55);
        }

        text-overflow: ellipsis;
        word-break: break-all;
        white-space: nowrap;
        width: 14rem;
        overflow: hidden;
    }

    .editor {
        @extend .title;

        background-color: transparent;
        color: white;
        width: 100%;
        font-size: 1rem;

        border: none;
        border-bottom: 1px solid white;

        &:focus {
            outline: none;
        }

        &:hover {
            border-bottom: 1px solid white;
        }
    }

</style>
