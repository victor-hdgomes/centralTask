<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import Greeting from '../../components/Greeting.vue'
import CreateEditTodo from '../../components/CreateEditTodo.vue'
import TodoList from '../../components/TodoList.vue'

const router = useRouter()
const todos = ref([])
const name = ref('')
const editTodo = ref(null)

const logout = () => {
	router.push('/login')
}

const addTodo = (todo) => {
	if (
		todo.title.trim() === '' ||
		todo.description.trim() === '' ||
		todo.dueDate === ''
	) {
		return
	}

	todos.value.push({
		title: todo.title,
		description: todo.description,
		dueDate: todo.dueDate,
		status: todo.status,
		userId: 'b4a76217-44e2-4f11-81ad-7c7a3b59f9ae'
	})
}

const updateTodo = (updated) => {
	const index = todos.value.findIndex((t) => t.id === updated.id)
	if (index !== -1) {
		todos.value[index] = updated
		saveTodos()
	}
	editTodo.value = null
}

const editExistingTodo = (todo) => {
	editTodo.value = { ...todo }
}

const removeTodo = (todo) => {
	todos.value = todos.value.filter((t) => t !== todo)
	saveTodos()
}

const saveTodos = () => {
	localStorage.setItem('todos', JSON.stringify(todos.value))
}

onMounted(() => {
	name.value = localStorage.getItem('name') || ''
	todos.value = JSON.parse(localStorage.getItem('todos')) || []
})
</script>

<template>
	<main class="app">
		<Greeting v-model="name" @logout="logout" />

		<CreateEditTodo :editTodo="editTodo" @add="addTodo" @update="updateTodo" />

		<TodoList :todos="todos" @remove="removeTodo" @edit="editExistingTodo" />
	</main>
</template>

<style src="./Dashboard.css" scoped></style>
