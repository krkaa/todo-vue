<template>
    <div class="todoLabel">
        <label
                v-show="toggled == false"
                @dblclick="toggled = true"
                class="label"
        >Note: <strong>{{notes.title}}</strong></label>
        <input v-show="toggled == true" v-model="note.title"
               v-on:blur="isCancel= true; toggled = false; $emit('update-note', notes.id, notes.title)"
               @keyup.enter="isCancel= true; toggled = false; $emit('update-note', notes.id, notes.title)">
        <button
                :disabled="!isCancel"
                @click="
                old = Object.assign({}, notes);
                $emit('update-note', cancelNote.id, cancelNote.title)"
        >&larr;
        </button>
        <button
                :disabled="isEmpty(old)"
                @click="$emit('update-note', old.id, old.title)"
        >&rarr;
        </button>
    </div>
</template>

<script>
    export default {
        name: "TodoLabel",
        props: {
            note: {
                type: Object,
                required: true
            }
        },
        data() {
            return {
                toggled: false,
                notes: this.note,
                cancelNote: Object.assign({}, this.note),
                isCancel: false,
                old: {}
            }
        },
        watch: {
            cancelNote: {
                deep: true
            }
        },
        methods: {
            isEmpty(obj) {
                return Object.keys(obj).length === 0;
            }
        }
    }
</script>

<style scoped>
    .todoLabel{ margin-top: 10px}
    .label {
        margin-right: 10px;
        font-size: 20px;
    }
</style>