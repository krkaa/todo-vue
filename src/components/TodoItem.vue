<template>
    <li>
        <span
                v-bind:class="{done: todo.completed}"
        >
            <input
                    type="checkbox"
                    v-on:change="todo.completed = !todo.completed"
                    v-bind:checked="todo.completed"
            >
            <strong>
                {{index + 1 + '.'}}
            </strong>
            <label
                    v-show="toggled == false"
                    @dblclick="toggled = true"
            >{{todo.title | uppercase}}</label>
            <input v-show="toggled == true" v-model="todos.title"
                   v-on:blur="toggled = false; $emit('update-todo', todo.id, todos.title)"
                   @keyup.enter="toggled = false; $emit('update-todo', todo.id, todos.title)">
        </span>
        <div>
            <!--<button
                    class="button"
                    v-on:click="$emit('remove-todo', todo.id)"
            >&times;
            </button>-->
            <ShowModal
                    v-on:delete="$emit('remove-todo', todo.id)"
                    v-bind:headerPhrase="'Are you sure to delete this task?' | uppercase"
            />
        </div>
    </li>
</template>

<script>
    import ShowModal from "./ShowModal";

    export default {
        props: {
            todo: {
                type: Object,
                required: true
            },
            index: Number
        },
        components: {
            ShowModal
        },
        data() {
            return {
                toggled: false,
                todos: this.todo,
                shouldShowDialog: false
            }
        },
        filters: {
            uppercase(value) {
                return value.toUpperCase()
            }
        }
    }
</script>

<style lang="scss" scoped>
    li {
        background: #f1f1f1;
        display: flex;
        justify-content: space-between;
        margin-bottom: 10px;
        padding: .3rem 2rem;
        position: relative;
        margin-bottom: 0;
        font-size: 20px;
        &:nth-child(2n) {
            background: #dcdada;
        }
    }

    input {
        margin-right: 1rem;
    }

    .done {
        text-decoration: line-through;
    }
</style>