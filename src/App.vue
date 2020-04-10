<template>
    <div id="app">
        <h1>My list</h1>
        <create-todo @add:todo="addTodo"/>
        <todo-list :todos="todos"
                   @delete:todo="deleteTodo"
                   @edit:todo="editTodo"/>
    </div>
</template>

<script>
    import TodoList from './components/TodoList.vue';
    import CreateTodo from './components/CreateTodo.vue';


    export default {
        name: 'App',
        components: {
            TodoList,
            CreateTodo
        },
        data() {
            return {
                todos: [
                    {
                        id: 1,
                        name: "Make a basic vue app",
                        description: "A basic crud app using VueJs."
                    }
                ]
            }
        },
        methods: {
            addTodo(todo) {
              console.log("App.vue", "addTodo", todo);
              const idOfLastTodo = this.todos.length > 0 ? (this.todos[this.todos.length - 1].id) : 0;
              const id = idOfLastTodo + 1;
              todo = {...todo, id};
              console.log("App.vue", "addTodo", idOfLastTodo, id, todo);
              this.todos = [...this.todos, todo];
            },

          editTodo(todoId, newTodo){
              this.todos = this.todos.map((todo) => {
                return todo.id === todoId ? newTodo : todo;
              })
            console.log("App.vue", "editTodo", todoId);

          },

          deleteTodo(todoId){
            console.log("App.vue", "deleteTodo", todoId);
            this.todos = this.todos.filter((todo) => todoId !== todo.id)
          }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        width: 80%;
        margin: 0 auto;
        padding: 20px;
    }
</style>
