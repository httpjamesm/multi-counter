<script lang="ts">
    import FaRegArrowAltCircleRight from 'svelte-icons/fa/FaRegArrowAltCircleRight.svelte'
</script>

<div class="bar">
    <div class="icon">
        <FaRegArrowAltCircleRight />
    </div>
</div>

<style lang="scss">
    .bar {
        width: 100%;
        height: 2rem;
        display: flex;
        justify-content: flex-end;
    }

    .icon {
        height: 2rem;
        width: 2rem;

        cursor: pointer;

        transition-duration: 512ms;

        &:hover {
            color: #949494;
        }
    }

</style>