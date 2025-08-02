<template>
    <section class="greeting">
        <h2 class="title">
            What's up, <input type="text" id="name" placeholder="Name here" :value="modelValue"
                @input="$emit('update:modelValue', $event.target.value)" />
        </h2>

        <button @click="logout" class="logout-button">Logout</button>
    </section>
</template>

<script setup>
defineProps({
    modelValue: {
        type: String,
        required: true
    }
})

const emit = defineEmits(['update:modelValue', 'logout']);

const logout = () => {
    emit('logout')
}
</script>

<style scoped>
.greeting {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1.5rem;
}

.greeting .title {
    display: flex;
}

.greeting .title input {
    margin-left: 0.5rem;
    flex: 1 1 0%;
    min-width: 0;
}

.greeting .title,
.greeting .title input {
    color: var(--dark);
    font-size: 1.5rem;
    font-weight: 700;
}

.logout-button {
    background-color: #333;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    margin-top: 0.5rem;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s;
}

.logout-button:hover {
    background-color: #555;
}
</style>
