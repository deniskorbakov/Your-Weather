<script setup>
    const props = defineProps({
        weather: {
            type: Object,
            required: true
        }
    })
</script>

<template>
    <div class="flex flex-row space-x-4 mt-5">
        <div class="basis-1/2">
            <div class="bg-gradient-to-r from-indigo-500 to-indigo-700 text-center p-5 rounded-lg h-full">
                <div>
                    <div class="flex flex-row">
                        <div class="basis-1/6 text-white p-5">
                            <i class="fa-solid fa-compass text-8xl"></i>
                        </div>

                        <div class="basis-5/6 text-white text-left ml-5">
                            <h3 class="text-xl font-bold">Longitude: {{weather.coord.lon}}</h3>
                            <p class="mt-2">Longitude measures distance east or west of the prime meridian.</p>

                            <h3 class="text-xl font-bold">Latitude: {{weather.coord.lat}}</h3>
                            <p class="mt-2">Latitude lines start at the equator (0 degrees latitude) and run east and west, parallel to the equator. </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="basis-1/2">
            <div class="bg-gradient-to-r from-indigo-500 to-indigo-700 text-center p-5 rounded-lg h-full">
                <div>
                    <div class="flex flex-row">
                        <div class="basis-1/6 text-white p-5">
                            <i class="fa-solid fa-droplet text-8xl"></i>
                        </div>

                        <div class="basis-5/6 text-white text-left ml-5">
                            <h3 class="text-xl font-bold">Humidity: {{weather.main.humidity}} %</h3>
                            <p class="mt-2">  Humidity is the concentration of water vapor present in the air. Water vapor, the gaseous state of water, is generally invisible to the human eye.</p>
                            <p class="mt-2">The same amount of water vapor results in higher relative humidity in cool air than warm air.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>

</style>