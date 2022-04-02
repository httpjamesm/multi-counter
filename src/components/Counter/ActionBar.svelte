<script lang="ts">
    import FaRegArrowAltCircleRight from "svelte-icons/fa/FaRegArrowAltCircleRight.svelte";

    import FaRegTrashAlt from "svelte-icons/fa/FaRegTrashAlt.svelte";

    import { Link } from "svelte-routing";

    export let id: number;

    import type Dexie from "dexie";

    export let db: Dexie;

    export let getCounters: () => void;

    const deleteCounter = async () => {
        await db["counters"].delete(id);
        await getCounters();
    };
</script>

<div class="bar">
    <div class="icon red" on:click={deleteCounter}>
        <FaRegTrashAlt />
    </div>
    <div class="icon">
        <Link to={`/counter?c=${id}`}>
            <FaRegArrowAltCircleRight />
        </Link>
    </div>
</div>

<style lang="scss">
    .bar {
        margin-top: .5rem;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .icon {
        height: 1.5rem;
        width: 1.5rem;

        cursor: pointer;

        transition-duration: 512ms;

        &:hover {
            color: #949494;
        }
    }

    .red {
        color: rgb(255, 113, 113);
    }
</style>
