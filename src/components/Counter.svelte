<script lang="ts">
    export let name = "Unnamed Counter";
    export let description = "No description yet.";
    export let color = "#ffffff";
</script>

<body>
    <div class="container">
        <div class="colorParent">
            <div class="color" style={`background: ${color}`} />
        </div>
        <div class="info">
            <p class="title">{name}</p>
            <p class="description">
                {description}
            </p>
        </div>
    </div>
</body>

<style>
    .container {
        width: 20rem;
        border-radius: 10px;
        border: 1px solid white;
        color: white;
        height: 5rem;
        padding: 1rem;
        display: flex;
        align-items: center;
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
    }

    .description {
        margin: 0;
        text-align: left;
    }
</style>
