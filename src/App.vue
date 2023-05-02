<script setup>

import {computed, onMounted, ref} from "vue";
import {API_KEY, BASE_URL} from "./constants";
import RightInfo from "./components/RightInfo/RightInfo.vue";
import BottomInfo from "./components/BottomInfo/BottomInfo.vue";

const weatherInfo = ref(null)
const city = ref('paris')



function getWeather() {
    fetch(`${BASE_URL}?q=${city.value}&units=metric&appid=${API_KEY}`)
        .then((response) => response.json())
        .then((data) => weatherInfo.value = data)
}

onMounted(getWeather)

const errors = computed(() => weatherInfo.value?.cod !== 200)
</script>

<template>
    <div v-if="errors" class="container mx-auto mt-56">
        <p class="text-white text-center uppercase">Error wrong name of the city</p>
        <input v-model="city" @keyup.enter="getWeather" type="text" id="email-address-icon" class="bg-white text-xl rounded-lg block w-full pl-10 p-2.5 text-black font-bold mt-5">
    </div>

    <div class="mt-10 p-5">
        <div class="flex flex-row space-x-4">
            <div class="basis-2/6">
                <div class="bg-gradient-to-r from-indigo-500 to-indigo-700 text-center p-5 rounded-lg h-full" v-if="!errors">
                    <div class="relative">
                        <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                            <i class="fa-solid fa-magnifying-glass text-white"></i>
                        </div>

                        <input v-model="city" @keyup.enter="getWeather" type="text" id="email-address-icon" class="bg-zinc-800 text-xl rounded-lg block w-full pl-10 p-2.5 text-white font-bold">
                    </div>

                    <div class="mt-5">
                        <div class="flex flex-row text-left">
                            <div class="basis-1/6">
                                <i class="fa-solid fa-temperature-half text-white text-4xl"></i>
                            </div>

                            <div class="basis-5/6 text-white">
                                <p class="font-bold uppercase text-4xl">{{Math.round(weatherInfo?.main.temp)}} °C</p>
                            </div>
                        </div>
                    </div>

                    <div class="mt-5 text-left">
                        <p class="font-bold text-2xl text-white">
                            {{weatherInfo.weather[0].description}}
                        </p>
                    </div>

                    <hr class="h-px my-8 bg-gray-200 border-0">

                    <div class="text-left">
                        <p class="font-bold text-md text-white">
                            <i class="fa-solid fa-map-pin"></i>
                            {{weatherInfo.name}}
                        </p>
                    </div>
                </div>
            </div>

            <div class="basis-4/6">
                <RightInfo v-if="!errors" :weather="weatherInfo"/>
            </div>
        </div>
        <BottomInfo :weather="weatherInfo" v-if="!errors"/>
    </div>
</template>

<style scoped>

</style>