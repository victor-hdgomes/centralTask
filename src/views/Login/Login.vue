<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useToast } from 'vue-toastification'

const toast = useToast()
const router = useRouter()

const email = ref('')
const password = ref('')

const loading = ref(false)
const error = ref(null)

async function login() {
    error.value = null

    if (!email.value || !password.value) {
        error.value = 'Please fill in email and password.'
        return
    }

    loading.value = true

    try {
        await fakeLogin(email.value, password.value)

        toast.success('Login successful!')

        router.push('/dashboard')
    } catch (err) {
        error.value = 'Invalid credentials.'
    } finally {
        loading.value = false
    }
}

function fakeLogin(email, password) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (email === 'email@example.com' && password === '123456') {
                resolve()
            } else {
                reject()
            }
        }, 1000)
    })
}
</script>

<template>
    <main class="login">
        <h2>Login</h2>
        <form @submit.prevent="login">
            <label for="email">Email</label>
            <input id="email" type="email" v-model="email" placeholder="email@example.com" required />

            <label for="password">password</label>
            <input id="password" type="password" v-model="password" placeholder="Your password" required />

            <p v-if="error" class="error-message">{{ error }}</p>

            <button type="submit" :disabled="loading">{{ loading ? 'Logging in...' : 'Log in' }}</button>
        </form>
    </main>
</template>

<style src="./Login.css" scoped></style>