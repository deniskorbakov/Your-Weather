<script setup>
    import {computed} from "vue";

    const props = defineProps({
        weather: {
            type: [Object, null],
            required: true
        }
    })
const getTime = (seconds) => {
    return new Date(seconds * 1000).toLocaleTimeString('ru-Ru', {timeZone: 'Atlantic/Reykjavik'})
}

const timeZone = computed(() => props.weather?.timezone)

const sunriseTime = computed(() => {
    return getTime(props.weather?.sys?.sunrise + timeZone.value);
})

const sunsetTime = computed(() => {
    return getTime(props.weather?.sys?.sunset + timeZone.value);
})
</script>

<template>
    <div class="bg-gradient-to-r from-indigo-500 to-indigo-700 text-center p-5 rounded-lg h-full">
        <div class="text-left">
            <h3 class="text-white text-3xl uppercase">Today's Highlights</h3>
        </div>

        <div class="flex flex-row mt-5 space-x-4">
            <div class="basis-1/3 bg-zinc-800 rounded-lg p-4">
                <div class="text-left">
                    <p class="text-white text-2xl">Wind</p>
                </div>

                <div class="text-center text-white text-5xl mt-5">
                    <i class="fa-solid fa-wind"></i>
                </div>

                <div class="flex justify-between mt-5">
                    <div>
                      <p class="text-white text-xl">{{weather.wind.speed}} m/s</p>
                    </div>

                    <div>
                        <p class="text-white text-xl">{{weather.wind.deg}} deg</p>
                    </div>
                </div>
            </div>

            <div class="basis-1/3 bg-zinc-800 rounded-lg p-4">
                <div class="text-left">
                    <p class="text-white text-2xl">Pressure</p>
                </div>

                <div class="text-center text-white text-5xl mt-5">
                    <i class="fa-solid fa-gauge"></i>
                </div>

                <div class="flex justify-between mt-5">
                    <div>
                    </div>
                    <div>
                        <p class="text-white text-xl">{{Math.round(weather.main.pressure * 0.750064)}} mm</p>
                    </div>
                    <div>
                    </div>
                </div>
            </div>

            <div class="basis-1/3 bg-zinc-800 rounded-lg p-4">
                <div class="text-left">
                    <p class="text-white text-2xl">Sunrise And Sunset</p>
                </div>

                <div class="text-center text-white text-5xl mt-5">
                    <i class="fa-solid fa-sun-plant-wilt"></i>
                </div>

                <div class="flex justify-between mt-5 text-left">
                    <div>
                        <h3 class="text-yellow-300 text-xl">Sunrise</h3>
                        <p class="text-white text-xl">{{sunriseTime}}</p>
                    </div>

                    <div>
                        <h3 class="text-yellow-300 text-xl">Sunset</h3>
                        <p class="text-white text-xl">{{sunsetTime}}</p>
                    </div>
                </div>
            </div>
        </div>

        <!--button dop info-->

        <div class="flex flex-row mt-5 space-x-4">
            <div class="basis-1/3 bg-zinc-800 rounded-lg p-4">
                <div class="text-white text-xl">
                    <p class="text-left">Wind Gusts</p>
                    <div v-if="weather.wind.gust">
                        <p class="text-center">{{weather.wind.gust}} m/s</p>
                    </div>
                    <div v-if="!weather.wind.gust">
                        <p class="text-center">no gust of wind</p>
                    </div>
                </div>
            </div>

            <div class="basis-1/3 bg-zinc-800 rounded-lg p-4">
                <div class="text-white text-xl">
                    <p class="text-left">Feels Like</p>
                    <p class="text-center">{{Math.round(weather.main.feels_like)}} °C</p>
                </div>
            </div>

            <div class="basis-1/3 bg-zinc-800 rounded-lg p-4">
                <div class="text-white text-xl">
                    <p class="text-left">Cloudiness</p>
                    <p class="text-center">{{weather.clouds.all}} %</p>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>

</style>