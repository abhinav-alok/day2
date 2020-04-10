<template>
    <div class="create-todo">
        <form @submit.prevent="createTodo">
            <label>Todo Name</label>
            <input type="text"
                   :class="{'has-error': submitting && invalidName}"
                   @focus="clearStatus"
                   @keypress="clearStatus"
                   v-model="todo.name"/>
            <label>Todo Description</label>
            <input type="text"
                   :class="{'has-error': submitting && invalidDescription}"
                   @focus="clearStatus"
                   v-model="todo.description"/>
            <p v-if="error && submitting" class="error-message">
                ❗Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
                ✅ Employee successfully added
            </p>
            <button id="add-todo-button">Add Todo</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: "CreateTodo",
        data(){
            return{
                submitting: false,
                error: false,
                success: false,
                todo: {
                    id: '',
                    name: '',
                    description: ''
                }
            }
        },
        computed: {
            invalidName(){
                return this.todo.name === '';
            },

            invalidDescription(){
                return this.todo.description === '';
            }
        },
        methods: {
            createTodo() {
                this.submitting = true;
                this.clearStatus();
                console.log("SUBMIT IS HANDLED");
                if(this.invalidName || this.invalidDescription){
                    this.error = true;
                    return
                }
                this.$emit('add:todo', this.todo);

                this.todo = {
                    name: '',
                    description: ''
                };

                this.error = false;
                this.submitting= false;
                this.success = true;
            },

            clearStatus(){
                this.success = false;
                this.error = false;
            }
        }
    }
</script>

<style scoped>
    form{
        margin-bottom: 2rem;
    }

    [class*='-message'] {
        font-weight: 500;
    }

    .error-message {
        color: #d33c40;
    }

    .success-message {
        color: #32a95d;
    }
</style>
