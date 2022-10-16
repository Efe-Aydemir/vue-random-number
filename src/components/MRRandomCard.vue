<template>
    <div id="root" class="flex justify-center items-center pt-10">
        <div class="bg-white px-40 py-5 rounded-xl shadow-lg shadow-black flex flex-col">
            <h1 class="text-xl ">Number</h1>
            <pre>{{number}}</pre>
            <button class="w-32 h-12 bg-black text-white" @click="basicnumber">click</button>
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue'

let number = ref(0)

function basicnumber() {
    number.value = Math.floor(Math.random() * 11);
}
</script>