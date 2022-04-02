<script lang="ts">
    import type Dexie from "dexie";
    import EditableColor from "./Counter/EditableColor.svelte";
import EditableDescription from "./Counter/EditableDescription.svelte";
    import EditableName from "./Counter/EditableName.svelte";

    export let name: string = "Unnamed Counter";
    export let description: string = "No description yet.";
    export let color: string = "#ffffff";
    export let id: number = 0;
    export let db: Dexie;
</script>

<body>
    <div class="container">
        <div class="colorParent">
            <EditableColor {db} {id} {color} />
        </div>
        <div class="info">
            <!-- make title an editable name component -->
            <EditableName {db} {id} {name} />
            <EditableDescription {db} {id} {description} />
        </div>
    </div>
</body>

<style lang="scss">
    .colorParent {
        width: 40%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }

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
    .info {
        width: 100%;
        padding-left: 1rem;
        height: 100%;
        display: flex;
        flex-direction: column;
    }
</style>
