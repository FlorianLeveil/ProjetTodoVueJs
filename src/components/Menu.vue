<template>
	<div class="todo-container">
			<div class="col">
				<input type="text" v-model="todoName" placeholder="Todo"/>
			</div>
			<div class="col">
				<input type="number" v-model="hours" placeholder="Hours"/>
			</div>
			<div class="col">
				<select v-model="worker">
					<option disabled value="">Select manager</option>
					<option>A</option>
					<option>B</option>
					<option>C</option>
				</select>
			</div>
			<div class="col-2">
				<button type="submit"  type="button" class="close" @click="addTodo()">submit</button>
			</div>
	</div>
</template>


<script>
export default {
	// eslint-disable-next-line vue/multi-word-component-names
	name: 'Menu',
	props: {
		msg: String
	},
	data() {
		return {
			worker: "",
			todoName: "",
			hours: 0,
			indexEditTodo: null,
			tempNameTodo: "",
			tempStatusTodo: "",
			todoStatus: ["to-do", "on-going", "finished"],
			todos: [],
		};
	},
	methods: {
		addTodo() {
			console.log(this.worker, this.todoName, this.hours)
			this.todos.push({
				name: this.todoName,
				status: "to-do",
				worker: this.worker,
				hours: this.hours,
			});
		}
	}
}
</script>

<style scoped>
.todo-container {
	width: 900px;
	text-align: initial;
}

.col {
	width: 200px;
	margin-left: 20x;
	margin-right: 20px;
	display: inline-block;
}

.col-2 {
	width: 100px;
	margin-left: 20x;
	margin-right: 20px;
	display: inline-block;
}
</style>
