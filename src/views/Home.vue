<template>
	<div class="home">
		<div class="addToDo">
			<input v-model="addToDoText" type="text"/>
			<button @click="create" class="create">Create</button>
		</div>
		<toDoList
			v-for = "item in toDoListItems"
			:key="item.id"
			:id="item.id"
			:text="item.text"
			@edit = "edit"
			@remove = "remove"
		/>
	</div>
</template>

<script>
// @ is an alias to /src
import toDoList from '@/components/toDoList.vue'

export default {
	name: 'home',
	components: {
		toDoList
	},
	data () {
		return {
			toDoListItems: [
				{
					id: 0,
					text: 'Read'
				},
				{
					id: 1,
					text: 'Wash the dishes'
				},
				{
					id: 2,
					text: 'Groceries'
				}
			],
			addToDoText: '',
			nextToDoId: 3
		}
	},
	mounted () {
		if (localStorage.getItem('personalToDoList') !== null) {
			this.toDoListItems = JSON.parse(localStorage.getItem('personalToDoList'))
		}
	},
	methods: {
		create () {
			this.toDoListItems.push({
				id: this.nextToDoId++,
				text: this.addToDoText.trim()
			})
			this.addToDoText = ''
			localStorage.setItem('personalToDoList', JSON.stringify(this.toDoListItems))
		},
		edit (id, editedText) {
			let item = this.toDoListItems.find(item => item.id === id)
			if (item) {
				item.text = editedText
			}
			localStorage.setItem('personalToDoList', JSON.stringify(this.toDoListItems))
		},
		remove (id) {
			this.toDoListItems.splice(this.toDoListItems.indexOf(id), 1)
			localStorage.setItem('personalToDoList', JSON.stringify(this.toDoListItems))
		}
	}
}
</script>

<style scoped lang="scss">
	.create {
		margin: 5px;
		bottom: 0;
		cursor: pointer;
		border-radius: 3px;
		border: 1px solid #e1e4e8;
  }
</style>
