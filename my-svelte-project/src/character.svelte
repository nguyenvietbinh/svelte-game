<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher()
    let character, characterX = 100,
     characterY = 370, characterDirection = {
        left: false,
        right: false,
        jumpping: false,
        onTheGround: true,
        falling: false,
     }, gravity = 0.5, velocity = 10, moveNextPage = false, numberOfHole, leftLimit = 4, rightLimit = 1166, bottomLimit = 370,
     isDeath = false, data, screenHeight, screenWidth, currentlyMap,isPass = false
    import { count, mapData, charX, charY } from "./store.js"
    count.subscribe(value => {
        currentlyMap = value
    })
    charX.subscribe(value => {
        characterX = value
        console.log(characterX)
    })
    charY.subscribe(value => {
        characterY = value
        console.log(characterY)
    })
    mapData.subscribe(value => {
        data = value
    })
    function sendData() {
        dispatch('sendData', [characterX, characterY, isDeath])
    }
    function move() {
        if (isPass) {
            characterX = 0
            isPass = false
            console.log(characterX, characterY)
            count.update(currentlyMap => {
                return currentlyMap+1
            })
            charX.update(characterX => {
                return characterX
            })            
            charY.update(characterY => {
                return characterY
            })
        }
        if (isDeath) {
            leftLimit = 4, rightLimit = 1166, bottomLimit = 370, characterX = 100, characterY = 370
            character.style.backgroundColor = 'black'
            bottomLimit = 370
            isDeath = false
            characterDirection.falling = false
        }
        if (!isDeath) {
            if (characterDirection.left) {
                if (characterX >= leftLimit) {
                    characterX -= 4
                }
            }
            if (characterDirection.right) {
                if (characterX <= rightLimit) {
                    characterX += 4
                }
            }
            if (characterDirection.jumpping && !characterDirection.falling) {
                characterY -= velocity
                velocity -= gravity
                if (characterY >= bottomLimit) {
                    characterDirection.jumpping = false
                    characterDirection.onTheGround = true
                    characterY = bottomLimit
                    velocity = 10
                }
            }
            if (characterDirection.falling) {
                velocity = 9
                bottomLimit = 570
                characterY += velocity
                if (characterY >= bottomLimit) {
                    characterDirection.falling = false
                    characterY = bottomLimit
                    velocity = 10
                }
            }
        }
        isDeathCheck()
        fall()
        sendData()
        isPassCheck()
        character.style.left = `${characterX}px`
        character.style.top = `${characterY}px`
        requestAnimationFrame(move)
    }
    function fall() {
        numberOfHole = data.hole.length/2
        for (let i = 0; i < numberOfHole; i ++) {
            if ((characterX >= data.hole[i]) && (characterX <= (data.hole[i] + data.hole[i+numberOfHole] - 30)) && characterDirection.onTheGround) {
                bottomLimit = 600
                leftLimit = data.hole[i] + 4
                rightLimit = data.hole[i] + data.hole[i+numberOfHole] - 34
                characterDirection.falling = true
            }
        }
    }
    function isPassCheck() {
        if (characterX >= 1166) {
            isPass = true
        }
    }
    function isDeathCheck() {
        if(characterY >= 560) {
            character.style.backgroundColor = 'red'
            isDeath = true
        }
    }
    import { onMount } from "svelte";
    onMount(() => {
        character = document.querySelector('.character')
        screenHeight = screen.height
        screenWidth = screen.width
        character.style.left = `${characterX}px`
        character.style.top = `${characterY}px`
        document.addEventListener('keydown', function(event) {
            if (event.keyCode === 65) {
                characterDirection.left = true
            }
            if (event.keyCode === 68) {
                characterDirection.right = true
            }
            if (event.keyCode === 32 || event.keyCode === 87) {
                if (!character.jumpping && !characterDirection.falling) {
                    characterDirection.jumpping = true
                    characterDirection.onTheGround = false
                }
            }
        })
        document.addEventListener('keyup', function(event) {
            if (event.keyCode === 65) {
                characterDirection.left = false
            }
            if (event.keyCode === 68) {
                characterDirection.right = false
            }
        })
        requestAnimationFrame(move)
        window.addEventListener('resize', function(event) {
            character.style.left = `${characterX}px`
            character.style.top = `${characterY}px`
        })
    })
</script>
<div class="character">
    <div class="rightEye"></div>
    <div class="leftEye"></div>
</div>
<style>
    .character {
        display: block;
        height: 30px;
        width: 30px;
        background-color: black;
        position: absolute;
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
</style>