<template>
    <div>
        <ul>
            <NoteItem
                    v-for="(note, index) of notes" :key="note.id"
                    v-bind:note="note"
                    v-bind:index="index"
                    v-bind:todo="todos"
                    v-on:remove-note="removeNote"
            />
        </ul>
    </div>
</template>

<script>
    import NoteItem from '@/components/NoteItem'

    export default {
        props: ['notes', 'todos'],
        name: 'NoteList',
        components: {
            NoteItem
        },
        methods: {
            removeNote(id) {
                this.$emit('remove-note', id)
            }
        }
    }
</script>

<style scoped>
    ul {
        list-style: none;
        padding: 0;
        margin: 0;
    }
</style>