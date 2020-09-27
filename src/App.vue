<template>
	<h1>Vue 3 Todo App</h1>
	<form @submit.prevent="addNewTodo">
		<label>New Todo</label>
		<input name="newTodo" v-model="newTodo" class="todo-input" />
		<button>Add New Todo</button>
	</form>
	<button @click="markAllDone">Mark All Todo List Done</button>
	<div class="todo-list">
		<ul>
			<li v-for="(todo, index) in todos" :key="todo.id">
				<h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
					{{ todo.content }}
				</h3>
				<button @click="removeTodo(index)">Remove</button>
			</li>
		</ul>
	</div>
</template>

<script>
import { ref } from "vue";

export default {
	setup() {
		const newTodo = ref("");
		const todos = ref([]);
		function addNewTodo() {
			if (newTodo.value === "") return null;
			todos.value.push({
				id: Date.now(),
				done: false,
				content: newTodo.value,
			});
			newTodo.value = "";
		}

		function toggleDone(todo) {
			todo.done = !todo.done;
		}

		function removeTodo(index) {
			todos.value.splice(index, 1);
		}

		function markAllDone() {
			if (todos.value === "") return null;
			todos.value.forEach((todo) => (todo.done = true));
		}

		return {
			newTodo,
			todos,
			addNewTodo,
			toggleDone,
			removeTodo,
			markAllDone,
		};
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

form {
	width: 80vw;
	margin: 1rem auto;
	display: flex;
	justify-content: space-evenly;
	align-items: center;
	font-size: 1.25rem;
}

label {
	font-weight: bold;
}

input {
	border: 2px solid #2c3e50;
	border-radius: 5px;
}

button {
	font-size: 1.1rem;
	font-weight: bold;
	border-radius: 5px;
	cursor: pointer;
}

.todo-input {
	width: 44vw;
	font-size: inherit;
}

.todo-list {
	margin: 2rem;
}

ul {
	text-align: start;
}

ul li h3 {
	display: inline-block;
	margin-right: 1rem;
	cursor: pointer;
}

.done {
	text-decoration: line-through;
}
</style>
