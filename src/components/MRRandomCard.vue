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
            <div class="music flex flex-col items-center p-5">
                <img v-if="musicview" @click="musicopen" src="@/assets/img/close.png" width="50" alt="Close" class="cursor-pointer"/>
                <img v-if="musicview===false" @click="musicoff" src="@/assets/img/open.png" width="50" alt="Open" class="cursor-pointer">
            </div>
        </div>
        <div class="inset-0 transition-all duration-1000 bg-white absolute flex justify-center items-center" :class="corr">
            <h1 class="text-5xl">{{restext}}</h1>
        </div>
    </div>
</template>

<script setup>
import {ref} from 'vue';
let music = require('@/assets/sounds/music.mp3')
let falsesound = require('@/assets/sounds/false.mp3')
let corsound = require('@/assets/sounds/correct.mp3')
let endsound = require('@/assets/sounds/end.mp3')
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
let musicview = ref(true)


let audio = new Audio(music)


function falsee() {
    let falseso = new Audio(falsesound)
    falseso.play()
}

function coreect() {
    let corree = new Audio(corsound)
    corree.play()
}

function end() {
    let endd = new Audio(endsound)
    endd.play()
}

function musicopen() {
    musicview.value = false
    audio.play()
}


function musicoff() {
    musicview.value = true
    audio.pause()
}


function easy() {
    islook.value = false
    islvllook.value = true
    eclick.value = true
    number.value = Math.floor(Math.random() * 11)
}

function normal() {
    islook.value = false
    islvllook.value = true
    nclick.value = true
    number.value = Math.floor(Math.random() * 51)
}

function hard() {
    islook.value = false
    islvllook.value = true
    hclick.value = true
    number.value = Math.floor(Math.random() * 101)
}

function menu() {
    islook.value = true
    islvllook.value = false
    number.value = 
    nclick.value = false
    eclick.value = false
    hclick.value = false
    heart.value = 5
    invalue.value = ''
}

function apply() {
    
    if(invalue.value === number.value) {
        restext.value = 'Correct'
        coreect()
        corr.value = 'opacity-100 visible'
        invalue.value = ''
        if (heart.value < 5) {
            heart.value += 1
        } else {
            heart.value = 5
        }
        if (eclick.value) {
        number.value = Math.floor(Math.random() * 11)

    } else if (nclick.value) {
        number.value = Math.floor(Math.random() * 51)
    } else if (hclick.value) {
        number.value = Math.floor(Math.random() * 101)
    }
    } else {
        restext.value = 'False'
        if (heart.value > 1) {
            falsee()
        } else {
            null
        }
        corr.value = 'opacity-100 visible'
        invalue.value = ''
        heart.value -= 1
        
    }

    if (heart.value < 1) {
        restext.value = 'Your life is over, you lost the game'
        end()
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
    }, 900);
}

</script>