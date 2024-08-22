<script>
    import HomePage from "./homePage.svelte";
    import MapOne from "./mapOne.svelte";
    import MapTwo from "./mapTwo.svelte";
    import UpdateData from "./updateData.svelte";
    import { count } from './store.js'

    let homePageDisplay = false, currentlyMap
    function handleDataFromHomePage(event) {
        homePageDisplay = event.detail
    }

    count.subscribe(value => {
        currentlyMap = value
    })
</script>
<UpdateData/>
<HomePage on:sendData={handleDataFromHomePage}/>
{#if homePageDisplay === true}
    {#if currentlyMap === 1}
        <MapOne/>
    {/if}
    {#if currentlyMap === 2}
        <MapTwo/>
    {/if}
{/if}