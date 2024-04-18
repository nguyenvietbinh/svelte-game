<script>
    import HomePage from "./homePage.svelte";
    import LevelOne from "./mapOne.svelte";
    import Demo from "./demo.svelte";
    let homePageDisplay = false
    function handleData(event) {
        homePageDisplay = event.detail
    }
</script>

<HomePage on:sendData={handleData}/>

{#if homePageDisplay === true}
    <LevelOne />
{/if}