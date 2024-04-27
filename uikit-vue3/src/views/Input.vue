<template>
    <h1 class="heading-1">Inputs</h1>
    <form @submit.prevent="submitForm">
        <Input
            label="Your email"
            name="email"
            placeholder="Введите ваш email"
            v-model:value="v.emailField.$model"
            :error="v.emailField.$errors"
        />
        <Input
            label="Your name"
            name="name"
            placeholder="Введите ваше имя"
            v-model:value="v.nameField.$model"
            :error="v.nameField.$errors"
        />
        <Input
            label="Your number"
            name="number"
            placeholder="Введите ваше любимое число"
            v-model:value="v.numField.$model"
            :error="v.numField.$errors"
        />
        <Input
            label="Your password"
            name="password"
            placeholder="Введите ваш пароль"
            v-model:value="passwordField"
            type="password"
        />
        <Input
            label="Your password"
            name="password"
            placeholder="Повторите ваш пароль"
            v-model:value="v.confirmPassword.$model"
            type="password"
            :error="v.confirmPassword.$errors"
        />
        <Input
            label="Your word"
            name="word"
            placeholder="Напишите ваше слово"
            v-model:value="v.frontendField.$model"
            :error="v.frontendField.$errors"
        />

        <Button label="Submit" color="primary">Отправить</Button>
    </form>
</template>

<script setup>
import { ref, computed } from 'vue';
import Input from '../components/Input.vue';
import Button from '../components/Button.vue';
import useVuelidate from '@vuelidate/core';
import { maxLength, minLength, required, helpers, email, numeric, sameAs } from '@vuelidate/validators';

const nameField = ref('')
const emailField = ref('')
const numField = ref('')
const passwordField = ref('')
const confirmPassword = ref('')
const frontendField = ref('')

const mustBeFrontend = (value) => value.includes('frontend')

const rules = computed(() => ({
    nameField: {
        minLength: helpers.withMessage('Минимум 3 символа', minLength(3))
    },
    emailField: {
        email: helpers.withMessage('Вы ввели неверный email', email)
    },
    numField: {
        numeric: helpers.withMessage('Только цифры', numeric),
        maxLength: helpers.withMessage('Максимум 6 символов', maxLength(6))
    },
    confirmPassword: {
        sameAsPassword: helpers.withMessage('Пароль не совпадает', sameAs(passwordField.value)),
    },
    frontendField: {
        frontendField: helpers.withMessage('Строка должна содержать слово frontend', mustBeFrontend)
    }
}))

const v = useVuelidate(rules, {nameField, emailField, numField, confirmPassword, frontendField})

const submitForm = () => {
    v.value.$touch()
    if (v.value.$error) return
    alert('Форма отправлена')
}
</script>