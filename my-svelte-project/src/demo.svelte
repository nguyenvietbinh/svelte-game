<script>
    let count, buttonClicked = false, button
    count = Math.floor(Math.random() * 10)
    import { onMount } from "svelte";
    onMount(() => {
        button = document.querySelector('.bt')
        button.addEventListener('click', function() {
            buttonClicked = true
        })
    })
    if (buttonClicked) {
        console.log(count)
    }
</script>
{#if buttonClicked}
    <script>
        console.log('as')
    </script>
    
{/if}
<div class="bt"></div>

<style>
    .bt {
        display: block;
        width: 1px;
        height: 1px;
        border-left: 15px solid transparent;
        border-right: 15px solid transparent;
        border-top: 30px solid red;
        position: absolute;
        top: 100px;
        left: 100px;
    }
</style>
