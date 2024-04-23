<template>
    <h1 class="heading-1">Checkbox</h1>
    <h2 class="heading-2">Checkbox Active</h2>
    <div class="line">
        {{ checkboxActive }}
        <checkbox
            label="Checkbox Active"
            id="checkboxActive"
            name="checkboxActive"
            value="I like"
            v-model:checked="checkboxActive"
        />
    </div>
    <h2 class="heading-2">Checkbox Disabled</h2>
    <div class="line">
        <checkbox
            label="Checkbox Disabled"
            id="checkboxDisabled"
            name="checkboxDisabled"
            value="I like"
            :disabled="checkboxDisabled"
            v-model:checked="checkboxDisabledChecked"
        />
    </div>
    <h2 class="heading-2">Checkbox Group</h2>
    <div class="line line_block">
        <p>Selected Heroes: {{ selectedHeroes }}</p>
        <checkbox-group
            :options="listOfHeroes"
            name="heroes"
            v-model:value="selectedHeroes"
        />
    </div>
    <h2 class="heading-2">Switch</h2>
    <div class="line line_block">
        <p>Switch: {{ switchProfessional }}</p>
        <checkbox
            label="I'm a professional"
            id="switch"
            name="switch"
            value="I'm a professional"
            type="switch"
            v-model:checked="switchProfessional"
        />
    </div>
</template>

<script setup>
import { ref } from 'vue'
import Checkbox from '@/components/Checkbox/Checkbox.vue'
import CheckboxGroup from '@/components/Checkbox/CheckboxGroup.vue'

const checkboxActive = ref(true)
const checkboxDisabled = ref(true)
const checkboxDisabledChecked = ref(true)
const selectedHeroes = ref([])

const listOfHeroes = ref([
    {name: 'Spider Man', id: 'h1'},
    {name: 'Batman', id: 'h2'},
    {name: 'Tor', id: 'h3'},
    {name: 'Loki', id: 'h4'},
  ])

const switchProfessional = ref(false)
</script>