<template>
    <h1 class="heading-1">Progress</h1>
    <h2 class="heading-2">Progress Bar</h2>
    <div class="line line_block">
        <ProgressBar maxWidth="500px" :percent="percentBar" color="success"/>
        <Button label="Add 10%" @click="addPercent"/>
    </div>
    <div class="line line_block">
        <h2 class="heading-2">Progress Circle</h2>
        <ProgressCircle :percent="percentCircle" color="danger"/>
        <Button label="Add 10%" @click="addCircle"/>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import ProgressBar from '../components/Progress/ProgressBar.vue';
import ProgressCircle from '../components/Progress/ProgressCircle.vue';
import Button from '../components/Button.vue'

const percentBar = ref(40)
const percentCircle = ref(60)

const addPercent = () => {
    percentBar.value += 10
    if (percentBar.value > 100) {
        percentBar.value = 100
    }
}

const addCircle = () => {
    percentCircle.value += 10
    if (percentCircle.value > 100) {
        percentCircle.value = 100
    }
}
</script>