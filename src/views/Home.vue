<template>
    <div>
        <h2>Home page</h2>
        <AddNote
                v-if="notes.length"
                v-bind:lastId="lastId"
                @add-note="addNote"
        />
        <hr>
        <Loader v-if="loading" />
        <NoteList
                v-else="notes.length"
                v-bind:notes="notes"
                @remove-note="removeNote"
        />
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
                loading: true
            }
        },
        components: {
            Loader, NoteList, AddNote
        },

        mounted() {
            fetch('https://my-json-server.typicode.com/krkaa/todo-vue/notes?_embed=todos')
                .then(response => response.json())
                .then(json => {
                    this.notes = json
                    this.loading = false
                })
        },
        computed: {
          lastId() {
              return this.notes[this.notes.length - 1].id
          }
        },
        methods: {
            removeNote(id) {
                fetch(`https://my-json-server.typicode.com/krkaa/todo-vue/notes/${id}`, {
                    method: 'DELETE',
                    headers: {
                        'Content-type': 'application/json; charset=UTF-8'
                    }
                })
                .then(res => res.json())
                .then(res => {
                    this.notes = this.notes.filter(item => item.id !== id)
                })
            },
            addNote(note) {
                console.log(note)
                this.notes.push(note)
            }
        }
    }
</script>