<template>
	<div class="to-do-list-item">
		<div v-if="editMode === true">
			<input type="text" v-model="addToDoText"/>
			<button @click="save" class="save">Save</button>
		</div>
		<div v-else>
			<span>{{text}}</span>
			<br>
			<button @click="edit" class="edit">Edit</button>
		</div>
		<button @click="remove" class="remove">Remove</button>
	</div>
</template>

<script>
export default {
	name: 'toDoList',
	props: {
		id: {
			type: Number,
			rquired: true
		},
		text: {
			type: String,
			rquired: true
		}
	},
	data () {
		return {
			editMode: false,
			addToDoText: ''
		}
	},
	methods: {
		edit () {
			this.addToDoText = this.text
			this.editMode = true
		},
		save () {
			this.$emit('edit', this.id, this.addToDoText)
			this.editMode = false
		},
		remove () {
			/* emit event to parent to remove the list item */
			this.$emit('remove', this.id)
		}
	}
}
</script>

<style scoped lang="scss">
.to-do-list-item {
  position: relative;
  border: 1px solid #3a2e47;
  border-radius: 10px;
  width: 300px;
  height: 50px;
  margin: 10px auto;
  padding:10px;
  box-sizing: border-box;
}
button {
    position: absolute;
    margin: 5px;
    bottom: 0;
    border-radius: 3px;
    border: 1px solid #ceb8e6;
  }
.edit {
	left: 0;
}
.save {
	left: 0;
}
.remove {
	right: 0;
}
</style>
