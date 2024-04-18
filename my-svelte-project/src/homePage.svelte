
<script>
    let textElement, containerElement, data = true
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher()
    function sendData() {
        dispatch('sendData', data)
    }
    import { onMount } from "svelte";
    onMount(() => {
        textElement = document.querySelector('.text')
        containerElement = document.querySelector('.container')
        textElement.addEventListener('click', function (event) {
            sendData()
            containerElement.style.display = 'none'
            textElement.style.display = 'none'
        })
        document.addEventListener('keydown', function() {
            sendData()
            containerElement.style.display = 'none'
            textElement.style.display = 'none'
        })
    })
    
</script>
<div class="container">
    <p class="text">Click Here To Play!</p>
</div>

<style>
    .container {
        display: block;
        background-color: rgb(189, 189, 189);
        height: 100%;
        width: 100%;
        position: absolute;
        top: 0px;
        left: 0px;
    }
    .text {
        display: block;
        font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
        font-size: 50px;
        position: absolute;
        margin: 0%;
        top: calc(50% - 50px);
        left: calc(50% - 200px);
    }
    .text:hover {
        text-decoration: underline;
    }
</style>