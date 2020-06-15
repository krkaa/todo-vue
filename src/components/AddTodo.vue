<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button class="btnAdd">Add task</button>
    </form>
</template>

<script>
    export default {
        props: {
            id: Number
        },
        data() {
            return {
                title: ''
            }
        },
        methods: {
            onSubmit() {
                if (this.title.trim()) {
                    const newTodo = {
                        noteId: this.id,
                        id: Date.now(),
                        title: this.title,
                        completed: false
                    }
                    this.$emit('add-todo', newTodo)
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