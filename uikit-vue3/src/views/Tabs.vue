<template>
    <h1 class="heading-1">Tabs</h1>
    <Tabs
        :names="tabs"
        :selectedTab="selectedTab"
        @changeTab="changeTab"
    >
        <div v-if="selectedTab === 'About'">1</div>
        <div v-if="selectedTab === 'Vue'">2</div>
        <div v-if="selectedTab === 'React'">3</div>
    </Tabs>
</template>

<script setup>
import { ref } from 'vue'
import Tabs from '../components/Tabs.vue';

const tabs = [
    {
        name: 'About',
        label: 'О проекте'
    },
    {
        name: 'Vue',
        label: 'про Vue'
    },
    {
        name: 'React',
        label: 'про React'
    },
]

const selectedTab = ref('Vue')

const changeTab = (tabName) => {
    selectedTab.value = tabName
}
</script>

