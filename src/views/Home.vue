<template>
    <div>
        <h2>Home page</h2>
        <AddNote
                v-bind:lastId="lastId"
                @add-note="addNote"
        />
        <hr>
        <Loader v-if="loading"/>
        <NoteList
                v-else-if="notes.length"
                v-bind:notes="notes"
                v-bind:todos="todos"
                @remove-note="removeNote"
        />
        <p v-else>
            List of note is empty, type note in input and press button for add note
        </p>
    </div>
</template>

<script>
    import Loader from '@/components/Loader'
    import NoteList from "../components/NoteList";
    import AddNote from "../components/AddNote";

    export default {
        name: 'Home',
        data() {
            return {
                notes: [],
                loading: true,
                newNote: '',
                todos: []
            }
        },
        components: {
            Loader, NoteList, AddNote
        },
        mounted() {
            if (localStorage.getItem('notes')) {
                this.notes = JSON.parse(localStorage.getItem('notes'))
                if (localStorage.getItem('todos')) {
                    this.todos = JSON.parse(localStorage.getItem('todos'))
                }
            }
            this.loading = false
        },
        watch: {
            notes: {
                handler() {
                    localStorage.setItem('notes', JSON.stringify(this.notes));
                },
                deep: true,
            }
        },
        computed: {
            lastId() {
                return this.notes.length !== 0
                    ? this.notes[this.notes.length - 1].id
                    : 0
            }
        },
        methods: {
            removeNote(id) {
                this.notes = this.notes.filter(item => item.id !== id)
                this.todos = this.todos.filter(item => item.noteId !== id)
                localStorage.setItem('todos', JSON.stringify(this.todos))
            },
            addNote(note) {
                this.notes.push(note)
                this.newNote = '';
            }
        }
    }
</script>