<script>
    export let table;
    export let active = -1;
</script>

<div id="tape">
    {#each table as cell, i}
        <div class="cell" class:active={i==active}>{cell}</div>
    {/each}
</div>

<style>
    .cell {
        border: 1px solid #000;
        padding-top: 15px;
        padding-bottom: 15px;
        background-color: #444;
        border-radius: 20px;
        color: #0f0;
        text-align: center;
        font-family: "Fira Code";
        width: 8vw;
        margin-top: 2vh;
        margin-bottom: 3vh;
    }
    #tape {
        display: flex;
        justify-content: space-evenly;
        width: 75%;
        margin-bottom: 2vh;
        margin: auto;
    }
    .active {
        background-color: #343;
    }
</style>
