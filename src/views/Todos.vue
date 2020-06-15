<template>
    <div>
        <router-link to="/">Home</router-link>
        <hr>
        <select v-model="filter">
            <option value="all">all</option>
            <option value="complete">complete</option>
            <option value="not-complete">not complete</option>
        </select>
        <AddTodo
                v-bind:id="id"
                @add-todo="addTodo"
        />
        <hr>
        <Loader v-if="loading"/>
        <TodoList
                v-else-if="filteredTodos.length"
                v-bind:todos="filteredTodos"
                @remove-todo="removeTodo"
        />
        <p v-else>
            List of task is empty
        </p>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddTodo from '@/components/AddTodo'
    import Loader from '@/components/Loader'
    import data from '../data.json'

    export default {
        name: 'Todos',
        data() {
            return {
                todos: [],
                loading: true,
                filter: 'all',
                id: +this.$route.params.id
            }
        },
        components: {
            TodoList, AddTodo, Loader
        },
        computed: {
            filteredTodos() {
                if (this.filter === 'all') {
                    return this.todos
                }

                if (this.filter === 'complete') {
                    return this.todos.filter(i => i.completed)
                }

                if (this.filter === 'not-complete') {
                    return this.todos.filter(i => !i.completed)
                }
            }
        },
        mounted() {
            //fake json with fake latency
            setTimeout(() => {
                Object.keys(data).map(i => data[i].noteId === this.id
                    ? this.todos.push(data[i])
                    : undefined
                )
                console.log(this.todos)
                this.loading = false
            }, 1000)
        },
        methods: {
            removeTodo(id) {
                this.todos = this.todos.filter(item => item.id !== id)
            },
            addTodo(task) {
                console.log(task)
                this.todos.push(task)
            }
        }
    }
</script>