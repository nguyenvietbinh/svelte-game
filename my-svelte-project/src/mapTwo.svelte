<script>
    let characterX, isDeath, characterY, data = {
    hole: [600, 200],
    object: [700, 100, 50, 900, 100, 50]
    }, currentlyMap
    import Character from "./character.svelte";
    import { count, mapData } from './store.js'
    count.subscribe(value => {
        currentlyMap = value
    })
    function handleData(event) {
        characterX = event.detail[0]
        characterY = event.detail[1]
        isDeath = event.detail[2]
    }
</script>

<div class="backGround">
    <div class="stage">
        <div class="hole"></div>
        <div class="object1"></div>
        <div class="object2"></div>
        {#if currentlyMap === 2}
            <Character mapTwoData={data} on:sendData={handleData}/>
        {/if}
        <div class="page">2</div>
    </div>
</div>

<style>
    .backGround {
        display: block;
        height: 100%;
        width: 100%;
        background-color: rgb(90, 90, 90);
        position: absolute;
        top: 0px;
        left: 0px;
    }
    .stage {
        display: block;
        height: 400px;
        width: 1198px;
        background-color: rgb(180, 180, 180);
        position: absolute;
        left: calc(50% - 600px);
        top: calc(50% - 300px);
    }
    .hole {
        display: block;
        width: 600px;
        height: 200px;
        background-color: rgb(180, 180, 180);
        position: absolute;
        top: 400px;
        left: 500px;
    }
    .object1 {
        display: block;
        width: 100px;
        height: 50px;
        background-color: rgb(90, 90, 90);
        position: absolute;
        left: 600px;
        top: 450px;

    }
    .page {
        display: block;
        font-size: 100px;
        position: absolute;
        margin-top: 0%;
        top: 0px;
        left: 0px;
    }
</style>