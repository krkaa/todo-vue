<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button class="btnAdd">Add note</button>
    </form>
</template>

<script>
    export default {
        props: {
            lastId: Number
        },
        data() {
            return {
                title: ''
            }
        },
        methods: {
            onSubmit() {
                if (this.title.trim()) {
                    const newNote = {
                        id: this.lastId + 1,
                        title: this.title
                    }
                    this.$emit('add-note', newNote)
                    this.title = ''
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    form {
        display: flex;

        input {
            margin-right: 10px;
            width: 50%;
            padding: .2rem .5rem;
        }
    }
</style>