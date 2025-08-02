<script setup>
import { defineProps, defineEmits, computed } from 'vue'

const props = defineProps({
    todos: {
        type: Array,
        required: true
    }
})

const emit = defineEmits(['remove', 'edit'])

const todos_asc = computed(() => {
    return props.todos.slice().sort((a, b) => {
        return new Date(a.dueDate).getTime() - new Date(b.dueDate).getTime()
    })
})

const statusMap = {
    0: 'Pending',
    1: 'InProgress',
    2: 'Completed'
}
</script>

<template>
    <section v-if="todos_asc.length" class="todo-list">
        <h3>TODO LIST</h3>

        <div class="list" id="todo-list">
            <div v-for="(todo, index) in todos_asc" :key="index" :class="`todo-item ${todo.status === 2 ? 'done' : ''}`"
                @click="emit('edit', todo)">
                <label>
                    <span class="bubble" :class="todo.status === 2 ? 'business' : 'personal'"></span>
                </label>

                <div class="todo-content">
                    <p class="todo-info">{{ todo.title }}</p>

                    <p class="todo-info">{{ statusMap[todo.status] || 'Unknown' }}</p>
                </div>

                <div class="actions">
                    <p class="todo-date">
                        {{ todo.dueDate }}
                    </p>

                    <button class="delete" @click.stop="$emit('remove', todo)">Delete</button>
                </div>
            </div>
        </div>
    </section>

    <section v-else class="empty-state">
        <p>No todos available</p>
    </section>
</template>

<style scoped>
.todo-list .list {
    margin: 1rem 0;
}

.todo-list .todo-item {
    display: flex;
    align-items: center;
    background-color: #FFF;
    cursor: pointer;
    padding: 1rem;
    border-radius: 0.5rem;
    box-shadow: var(--shadow);
    margin-bottom: 1rem;
}

.todo-item label {
    display: block;
    margin-right: 1rem;
    cursor: pointer;
}

.todo-item .todo-content {
    flex: 1 1 0%;
    display: flex;
    flex-direction: row;
    gap: 1rem;
    align-items: center;
}

.todo-info {
    flex: 2;
    color: var(--dark);
    font-size: 1.125rem;
}

.todo-item .actions {
    display: flex;
    gap: 20px;
    align-items: center;
}

.todo-item .actions button {
    display: block;
    padding: 0.5rem;
    border-radius: 0.25rem;
    color: #FFF;
    cursor: pointer;
    transition: 0.2s ease-in-out;
}

.todo-item .actions button:hover {
    opacity: 0.75;
}

.todo-item .actions .delete {
    background-color: var(--danger);
}

.todo-item.done .todo-content input {
    text-decoration: line-through;
    color: var(--grey);
}

.empty-state {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 150px;
}

@media (max-width: 790px) {
    .todo-list .todo-item {
        flex-direction: column;
        align-items: stretch;
    }

    .todo-item label {
        margin-bottom: 0.5rem;
    }

    .todo-item .todo-content {
        flex-direction: column !important;
        gap: 0.5rem;
        align-items: stretch;
    }

    .todo-info {
        flex: none !important;
        width: 100%;
        font-size: 1rem;
        margin-bottom: 0.5rem;
    }

    .todo-item .actions {
        flex-direction: column;
        gap: 0.5rem;
        align-items: stretch;
        margin-top: 0.5rem;
    }

    .todo-date {
        width: 100% !important;
    }

    .todo-item .actions button {
        width: 100%;
    }
}
</style>
