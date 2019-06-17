<template>
	<div id="app">
		<h1 class="text-5xl font-sans">{{ title }}</h1>
		<input type="text" placeholder="Add todo…" v-on:keyup.enter="addTodo" />
		<ul>
			<li v-for="todo in todos" class="flex" v-bind:key="todo.id">
				<input
					type="checkbox"
					class="pr-10"
					v-on:click="check(todo)"
					v-bind:checked="todo.done"
				/>
				<span v-bind:class="{ 'line-through': todo.done }">{{
					todo.text
				}}</span>
				<button class="pl-10" v-on:click="removeTodo(todo.id)">X</button>
			</li>
		</ul>
		<img alt="Vue logo" src="./assets/logo.png" />
		<HelloWorld msg="Welcome to Your Vue.js App" />
	</div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
	name: 'app',
	data: function() {
		return {
			title: 'todoist',
			todos: [],
		}
	},
	methods: {
		addTodo(event) {
			const text = event.target.value
			this.todos.push({
				text,
				done: false,
				id:
					'_' +
					Math.random()
						.toString(36)
						.substr(2, 9),
			})
			event.target.value = ''
		},
		removeTodo(id) {
			this.todos = this.todos.filter(todo => todo.id !== id)
		},
		check(todo) {
			todo.done = !todo.done
		},
	},
	components: {
		HelloWorld,
	},
}
</script>

<style>
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
