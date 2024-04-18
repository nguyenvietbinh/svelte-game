<script>
    let characterX, characterY, hole1, hole2, data = {
        hole: [900, 200, 100, 100]
    }
    import Character from "./character.svelte";
    function handleData(event) {
        characterX = event.detail[0]
        characterY = event.detail[1]
    }
    function holeIsOpen() {
        if(characterX >= 190) {
            hole1.style.display = 'block'
        }
        if(characterX >= 800) {
            hole2.style.display = 'block'
        }
        requestAnimationFrame(holeIsOpen)
    }
    import { onMount } from "svelte";
    onMount(() => {
        hole1 = document.querySelector('.hole1')
        hole2 = document.querySelector('.hole2')
        requestAnimationFrame(holeIsOpen)
    })
</script>

<div class="backGround">
    <div class="stage">
        <div class='goal'>
            <div class="rightEye"></div>
            <div class="leftEye"></div>
        </div>
        <div class="hole1"></div>
        <div class="hole2"></div>
        <Character mapOneData={data} on:sendData={handleData}/>
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
    .goal {
        display: block;
        height: 30px;
        width: 30px;
        background-color: rgb(255, 0, 255);
        position: absolute;
        top: 370px;
        left: 1100px;
    }
    .rightEye {
        display: block;
        height: 5px;
        width: 5px;
        background-color: rgb(255, 255, 255);
        border-radius: 50%;
        position: absolute;
        top: 8px;
        left: 6px;
    }
    .leftEye {
        display: block;
        height: 5px;
        width: 5px;
        background-color: aliceblue;
        border-radius: 50%;
        position: absolute;
        top: 8px;
        right: 6px;
    }
    .hole2 {
        display: none;
        width: 100px;
        height: 200px;
        background-color: rgb(180, 180, 180);
        position: absolute;
        top: 400px;
        left: 900px;
    }
    .hole1 {
        display: none;
        width: 100px;
        height: 200px;
        background-color: rgb(180, 180, 180);
        position: absolute;
        top: 400px;
        left: 200px;
    }
</style>