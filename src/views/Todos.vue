<template>
    <div>
        <router-link to="/">Home</router-link>
        <TodoLabel
                v-if="seekNote"
                v-bind:note="seekNote"
                @update-note="updateNote"
        />
        <hr>
        <select v-model="filter" class="select">
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
                @update-todo="updateTodo"
        />
        <p v-else-if="err">This page not have a parent note! Please back to homepage and create a new note.</p>
        <p v-else>
            List of task is empty
        </p>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddTodo from '@/components/AddTodo'
    import Loader from '@/components/Loader'
    import TodoLabel from "../components/TodoLabel";

    export default {
        name: 'Todos',
        data() {
            return {
                todos: [],
                loading: true,
                filter: 'all',
                id: +this.$route.params.id,
                newTodo: '',
                notes: [],
                err: false
            }
        },
        components: {
            TodoLabel,
            TodoList,
            AddTodo,
            Loader
        },
        computed: {
            seekNote() {
                return this.notes.filter(i => i.id === this.id)[0]
            },
            filteredTodos() {
                if (this.filter === 'all') {
                    return this.todos.filter(i => i.noteId === this.id)
                }

                if (this.filter === 'complete') {
                    return this.todos.filter(i => i.completed && i.noteId === this.id)
                }

                if (this.filter === 'not-complete') {
                    return this.todos.filter(i => !i.completed && i.noteId === this.id)
                }
            }
        },
        mounted() {
            if (localStorage.getItem('notes')) {
                this.notes = JSON.parse(localStorage.getItem('notes'))
                const note = this.notes.filter(i => i.id === this.id)[0]
                if (note) {
                    if (localStorage.getItem('todos')) {
                        this.todos = JSON.parse(localStorage.getItem('todos'))
                    }
                    this.err = false
                } else {
                    this.err = true
                }
            } else {
                this.err = true
            }
            this.loading = false
        },
        watch: {
            todos: {
                handler() {
                    localStorage.setItem('todos', JSON.stringify(this.todos));
                },
                deep: true,
            },
            notes: {
                handler() {
                    localStorage.setItem('notes', JSON.stringify(this.notes));
                },
                deep: true,
            }
        },
        methods: {
            removeTodo(id) {
                this.todos = this.todos.filter(item => item.id !== id)
            },
            addTodo(task) {
                this.todos.push(task);
                this.newTodo = '';
            },
            updateTodo(id, title) {
                this.todos.forEach(item => item.id === id
                    ? item.title = title
                    : item.title)
            },
            updateNote(id, title) {
                this.notes.forEach(item => item.id === id
                    ? item.title = title
                    : item.title)
            }
        }
    }
</script>

<style scoped>
    .select {
        margin-bottom: 20px;
        padding: 3px;
        font-size: 20px;
        outline: none;
    }
</style>