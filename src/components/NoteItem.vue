<template>
    <li>
        <ul>
            <ol class="ol">
                <span>
                    <strong>
                        {{index + 1 + '.'}}
                    </strong>

                        <router-link :to="path" class="link">
                            {{note.title | uppercase}}
                        </router-link>
                </span>
                <ShowModal
                        v-on:delete="$emit('remove-note', note.id)"
                        v-bind:headerPhrase="'ARE you SURE to DELETE THiS NOTE?' | uppercase"
                />
            </ol>
            <li
                    v-for="(t,index) of filteredTodos" v-if="index < 3"
                    class="li"
            >
                <p class="todos" v-if="filteredTodos.length">{{index + 1 +'. '+t.title}}</p>
            </li>
        </ul>
    </li>
</template>

<script>
    import ShowModal from "./ShowModal";

    export default {
        props: {
            note: {
                type: Object,
                required: true
            },
            index: Number,
            todo: {
                type: Array,
                required: false
            }
        },
        data() {
            return {
                path: `todos/${this.note.id}`
            }
        },
        components: {
            ShowModal
        },
        computed: {
            filteredTodos() {
                if (this.todo) {
                    return this.todo.filter(item => item.noteId === this.note.id)
                }
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
    ul {
        margin: 0;
        padding: 0;
    }

    .ol {
        background: #f1f1f1;
        display: flex;
        justify-content: space-between;
        margin-bottom: 10px;
        padding: .3rem 2rem;
        position: relative;
        margin-bottom: 0;
        font-size: 20px;
    }

    .li {
        list-style-type: none;
        text-align: left;
        background: #959292;
        padding: .3rem 3rem;
        font-size: 18px;
        color: floralwhite;
        & .todos {
            margin: 0;
        }
        &:nth-child(2n) {
            background: #585757;
        }
    }

    .button {
        border-radius: 50%;
        line-height: 50%;
        border: none;
        font-weight: 600;
        background: #ff0000;
        outline: none;
        cursor: pointer;
        transition: background .15s ease-in-out;
        color: white;
        padding: 10px;

        &:hover {
            background: rgba(#ff0000, .6);
        }

        &:active {
            background: rgba(#ff0000, .4);
        }

        &.edt {
            margin-right: 10px;
            background: #228b22;

            &:hover {
                background: rgba(#228b22, .6);
            }

            &:active {
                background: rgba(#228b22, .4);
            }
        }
    }

    input {
        margin-right: 1rem;
    }

    .done {
        text-decoration: line-through;
    }

    a.link {
        text-decoration: none;
        margin-left: 10px;
        color: #0f0f0f;
        transition: color .1s ease-in;

        &:hover {
            color: rgba(#0f0f0f, .6);
        }

        &:active {
            color: rgba(#0f0f0f, .4);
        }
    }

    .dropdown {
        position: absolute;
        display: inline-block;
        transition: hover .15s ease-in;

        &-content {
            display: none;
            position: absolute;
            background-color: #f1f1f1;
            min-width: 160px;
            width: max-content;
            z-index: 1;
            text-align: left;
            padding: 10px 25px;
        }

        &a {
            color: black;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
        }

        &a:hover {
            background-color: #ddd
        }

        &:hover .dropdown-content {
            display: block;
        }
    }
</style>