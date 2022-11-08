<template>
    <div id="root" class="flex justify-center items-center pt-10">
        <div class="bg-white px-40 py-5 rounded-xl shadow-lg shadow-black flex flex-col">
            <div class="flex flex-col gap-5" v-if="islook">
                <button class="w-32 h-12 transition-all duration-300 bg-green-400 text-black rounded-xl hover:shadow-xl hover:shadow-black" @click="easy">easy level</button>
            <button class="w-32 h-12 bg-yellow-500 transition-all duration-300 text-black rounded-xl hover:shadow-xl hover:shadow-black" @click="normal">normal level</button>
            <button class="w-32 h-12 bg-red-700 text-white rounded-xl transition-all duration-300 hover:shadow-xl hover:shadow-black" @click="hard">hard level</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue';

let islook = ref(true)

function easy() {
    islook.value = false
}
</script>