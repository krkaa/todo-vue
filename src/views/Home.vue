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
    import notes from '../../notes.json'
    import data from '../../db.json'
    import Loader from '@/components/Loader'
    import NoteList from "../components/NoteList";
    import AddNote from "../components/AddNote";

    export default {
        name: 'Home',
        data() {
            return {
                notes: [],
                data: [],
                loading: true
            }
        },
        components: {
            Loader, NoteList, AddNote
        },

        mounted() {
            //fake json with fake latency
            console.log(data)
            setTimeout(() => {
                this.notes = notes
                this.data = data
                this.loading = false
            },1000)
        },
        computed: {
          lastId() {
              return this.notes[this.notes.length - 1].id
          }
        },
        methods: {
            removeNote(id) {
                this.notes = notes.filter(item => item.id !== id)
                this.data = this.data.filter(item => item.noteId !== id)
                console.log(this.notes)
            },
            addNote(note) {
                console.log(note)
                this.notes.push(note)
            }
        }
    }
</script>