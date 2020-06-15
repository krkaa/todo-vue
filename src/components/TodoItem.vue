<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input
                    type="checkbox"
                    v-on:change="todo.completed = !todo.completed"
            >
            <strong>
                {{index + 1}}
            </strong>
            {{todo.title | uppercase}}
        </span>
        <button
                class="button"
                v-on:click="$emit('remove-todo', todo.id)"
        >&times;</button>
    </li>
</template>

<script>
    export default {
        props: {
            todo: {
                type: Object,
                required: true
            },
            index: Number
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
        border: 1px solid #222222;
        display: flex;
        justify-content: space-between;
        margin-bottom: 10px;
        padding: .3rem 2rem;
    }

    .button {
        border-radius: 10rem;
        border: none;
        font-weight: 600;
        background: #ff0000;
        outline: none;
        cursor: pointer;
        transition: background .15s ease-in-out;
        color: white;
        &:hover {
            background: rgba(#ff0000, .6);
        }
        &:active {
            background: rgba(#ff0000, .4);
        }
    }

    input {
        margin-right: 1rem;
    }

    .done {
        text-decoration: line-through;
    }
</style>