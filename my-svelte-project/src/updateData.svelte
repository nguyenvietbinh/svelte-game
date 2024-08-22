<script>
    let mapOneData = {hole: [900, 200, 100, 100]},
        mapTwoData = {hole: [500, 500]},
        data = [mapOneData, mapTwoData]

    let currentlyMap
    import { count, mapData } from './store.js'
    mapData.set(data[0])
    count.subscribe(value => {
        currentlyMap = value
        mapData.set(data[currentlyMap-1])
    })
    console.log('as')
</script>

