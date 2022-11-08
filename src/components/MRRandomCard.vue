<template>
    <div id="root" class="flex justify-center items-center pt-10">
        <div class="bg-white px-20 py-5 rounded-xl shadow-lg shadow-black flex flex-col">
            <div v-if="islvllook" class="flex flex-col text-center gap-5">
                <h1>Number</h1>
                <input class="border-black text-2xl border-2 rounded-xl text-center mx-auto w-32" @keyup.enter="apply" type="number" v-model="invalue"/>
                <button class="w-32 h-12 bg-black text-white rounded-xl mx-auto" @click="apply">Apply</button>
                <button class="w-32 h-12 bg-black text-white rounded-xl mx-auto" @click="menu">Menu</button>
                <pre>Heart {{heart}}</pre>
            </div>
            <div class="flex flex-col gap-5" v-if="islook">
                <button class=" h-12 w-44 transition-all duration-300 bg-green-400 text-black rounded-xl hover:shadow-xl hover:shadow-green-800" @click="easy">easy level (0 to 10)</button>
            <button class="w-44 h-12 bg-yellow-500 transition-all duration-300 text-black rounded-xl hover:shadow-xl hover:shadow-yellow-800" @click="normal">normal level (0 to 50)</button>
            <button class="w-44 h-12 bg-red-700 text-white rounded-xl transition-all duration-300 hover:shadow-xl hover:shadow-red-900" @click="hard">hard level (0 to 100)</button>
            </div>
        </div>
        <div class="inset-0 transition-all duration-1000 bg-white absolute flex justify-center items-center" :class="corr">
            <h1 class="text-5xl">{{restext}}</h1>
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue';

let islook = ref(true)
let islvllook = ref(false)
let number = ref()
let eclick = ref(false)
let nclick = ref(false)
let hclick = ref(false)
let corr = ref('opacity-0 invisible')
let invalue = ref()
let restext = ref('')
let heart = ref(5)

function easy() {
    islook.value = false
    islvllook.value = true
    eclick.value = true
    number.value = Math.floor(Math.random() * 11)
        console.log(number.value)
}

function normal() {
    islook.value = false
    islvllook.value = true
    nclick.value = true
    number.value = Math.floor(Math.random() * 51)
        console.log(number.value)
}

function hard() {
    islook.value = false
    islvllook.value = true
    hclick.value = true
    number.value = Math.floor(Math.random() * 101)
        console.log(number.value)
}

function menu() {
    islook.value = true
    islvllook.value = false
    number.value = 
    nclick.value = false
    eclick.value = false
    hclick.value = false
    
    invalue.value = ''
}

function apply() {
    
    if(invalue.value === number.value) {
        restext.value = 'Correct'
        corr.value = 'opacity-100 visible'
        invalue.value = ''
        heart.value = 5
        if (eclick.value) {
        number.value = Math.floor(Math.random() * 11)
        console.log(number.value)
    } else if (nclick.value) {
        number.value = Math.floor(Math.random() * 51)
        console.log(number.value)
    } else if (hclick.value) {
        number.value = Math.floor(Math.random() * 101)
        console.log(number.value)
    }
    } else {
        restext.value = 'False'
        corr.value = 'opacity-100 visible'
        invalue.value = ''
        heart.value -= 1
    }

    if (heart.value < 1) {
        restext.value = 'Your life is over, you lost the game'
        islook.value = true
    islvllook.value = false
    number.value = 
    nclick.value = false
    eclick.value = false
    hclick.value = false
    
    invalue.value = ''
    heart.value = 5
    }

    setTimeout(() => {
        corr.value = 'opacity-0 invisible'
    }, 2000);
}

</script>