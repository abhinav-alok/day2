<template>
    <div class="todo-list">
        <template>
            <table>
                <thead>
                <tr>
                    <th>Sl. No</th>
                    <th>Todo Name</th>
                    <th>Todo Description</th>
                    <th>Actions</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(todo, i) in todos"
                    :key="todo.id">
                    <td>{{i + 1}}</td>
                    <td v-if="editingTodo === todo.id">
                        <input type="text" v-model="todo.name">
                    </td>
                    <td v-else>{{todo.name}}</td>
                    <td v-if="editingTodo === todo.id">
                        <input type="text" v-model="todo.description">
                    </td>
                    <td v-else>{{todo.description}}</td>
                    <td v-if="editingTodo === todo.id">
                        <button @click="saveTodo(todo)">Save</button>
                        <button @click="editingTodo = null">Cancel</button>
                    </td>
                    <td v-else>
                        <button @click="editTodo(todo.id)">Edit</button>
                        <button @click="$emit('delete:todo', todo.id, todo)">Delete</button>
                    </td>
                </tr>
                </tbody>
            </table>
        </template>
    </div>
</template>

<script>
    export default {
        name: 'TodoList',
        props: {
            todos: Array
        },
        data() {
            return {
                editingTodo: null
            }
        },
        methods: {
            editTodo(todoId) {
              console.log("TodoList.vue", "editTodo", todoId);
                this.editingTodo = todoId;
            },

            saveTodo(todo) {
                console.log("TodoList.vue", "saveTodo", todo);
                if (todo.name === '' || todo.description === '') return
                this.$emit('edit:todo', todo.id, todo)
                this.editingTodo = null
            },
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    button {
        margin: 0 0.5rem 0 0;
    }
</style>
