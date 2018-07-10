<template>

    <div>
        <div v-if="isEditing">
            <input v-model="editedText"></input>
            <button @click="submitEditedText">Submit</button>
        </div>
        <div v-else>
            {{ todo }}
            <!-- = renders in the template -->
            <button @click="editTodo">Edit</button>
            <button @click="deleteTodo">Delete</button>
        </div>
    </div>

</template>

<script>
export default {
    props: [ "todo" ],
    //vuejs property. a way to pass data from parent to child component.
    methods: {
        editTodo: function() {
            this.isEditing = true
            this.editedText = this.todo
        },
        submitEditedText: function() {
            this.$emit('textEdited', this.editedText)
            //emits an event called textEdited with a payload of the old value and the new value
            this.isEditing = false
        },
        deleteTodo: function() {
            this.$emit('buttonDeleted', this.todo)    
        }
    },
    data: function() {
            return {
                isEditing: false,
                editedText: '',
            }
        }
}
</script>
