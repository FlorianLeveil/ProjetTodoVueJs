<template>
	<div class="create-todo-container">
		<div class="col">
			<input class="w-100" type="text" v-model="todoName" placeholder="Todo"/>
		</div>
		<div class="col">
			<input class="w-100" type="number" v-model="hours" placeholder="Hours"/>
		</div>
		<div class="col">
			<select class="w-100" v-model="worker">
				<option disabled value="">Select manager</option>
				<option>A</option>
				<option>B</option>
				<option>C</option>
			</select>
		</div>
		<div class="col-2">
			<button class="w-100" type="submit" @click="addTodo()">submit</button>
		</div>
	</div>
	<div class="todo-container">
		<div class="todo-line" v-for="(todo, index) in todos" :key="index">
			<div>
				<input
					type="checkbox"
					v-model="todo.toggled"
					true-value="true"
					false-value="false"/>

				<span>{{ todo.name }}</span>
				<span>{{ todo.hours }}</span>
				<span>{{ todo.worker }}</span>
				<button type="submit" @click="updateTodo(index)">!!!Modifier!!!</button>
				<button type="submit" @click="removeTodo(index)">X</button>
				<button type="submit" @click="changeStatusTodo(index, todoStatus.FINISHED)">X</button>
			</div>
		</div>
	</div>

	<div>
		<button type="submit" @click="multiRemoveTodo()"> Remove all</button>
		<div>Selected: {{ this.todos.filter(todo => todo.toggled === "true").length }}</div>

	</div>
	<div>
		<div>Todo Create: {{ this.todos.length }}</div>

	</div>
</template>


<script>
export default {
	// eslint-disable-next-line vue/multi-word-component-names
	name: 'Todo',
	props: {
		msg: String
	},
	data() {
		return {
			worker: "",
			todoName: "",
			hours: 0,
			indexUpdateTodo: null,
			todos: [],
			todoStatus: {
				ON_GOING: 'on going',
				IN_PROGRESS: 'in progress',
				FINISHED: 'finished'
			},
			incrementMultiRemoveTodo: 0
		};
	},
	methods: {
		addTodo() {
			if (this.indexUpdateTodo) {
				this.todos[this.indexUpdateTodo].todoName = this.todoName;
				this.todos[this.indexUpdateTodo].hours = this.hours;
				this.todos[this.indexUpdateTodo].worker = this.worker;
				this.indexUpdateTodo = null;
			}
			this.todos.push({
				name: this.todoName,
				worker: this.worker,
				hours: this.hours,
				status: this.todoStatus.ON_GOING,
				toggled: false,
			});
		},
		removeTodo(index) {
			this.todos.splice(index, 1);
		},
		updateTodo(index) {
			this.todoName = this.todos[index].name;
			this.hours = this.todos[index].hours;
			this.worker = this.todos[index].hours;
			this.indexUpdateTodo = index;
		},
		multiRemoveTodo() {
			let todoToDel = []
			for (let i = 0; i < this.todos.length; i++) {
				if (this.todos[i].toggled) {
					todoToDel.push(i)
				}
			}
			if (todoToDel.length !== 0) {
				const reversedTodoToDel = todoToDel.reverse()
				for (let i = 0; i < reversedTodoToDel.length; i++) {
					this.removeTodo(reversedTodoToDel[i])
				}
			}

		},
		changeStatusTodo(index, status) {
			this.todos[index].status = status;
		}

	}
}
</script>

<style scoped>
.create-todo-container {
	width: 1000px;
	margin: auto;
	margin-bottom: 50px;
}

.todo-container {
	margin: auto;
	width: 1000px;
	background-color: #2c3e50;
	height: 700px;
	max-height: 700px;
	border-radius: 20px;
	text-align: center;
	overflow: auto;
}
.todo-line {
	height: 35px;
	background-color: rgba(0, 0, 0, 0.98);
	width: 100%;
	margin-bottom: 5px;
	text-align: initial;
}

.col {
	width: 250px;
	display: inline-block;
	margin-left: 10px;
	margin-right: 10px;
}

.w-100 {
	width: 100%;
}

.col-2 {
	width: 100px;
	margin-left: 20x;
	margin-right: 20px;
	display: inline-block;
}
</style>
