<script lang="ts">
    import type Dexie from "dexie";

    export let color: string = "#ffffff";

    export let id: number;

    export let db: Dexie;

    const cycle = [
        "#ffffff",
        "#ff0000",
        "#ff7f00",
        "#ffff00",
        "#00ff00",
        "#00ffff",
        "#0000ff",
        "#7f00ff",
        "#ff00ff",
        "#ff0000",
    ];

    let cyclePos = cycle.indexOf(color);

    const cycleColor = () => {
        cyclePos = (cyclePos + 1) % cycle.length;
        color = cycle[cyclePos];

        // update the counter id
        db["counters"].update(id, {
            color,
        });
    };
</script>

<div
    class="color"
    style={`background: ${cycle[cyclePos]}`}
    on:click={cycleColor}
/>

<style lang="scss">
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
</style>
