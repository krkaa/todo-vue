<template>
    <div>
        <li>
            <span>
            <strong>
                {{index + 1}}
            </strong>
            <router-link :to="path">
                {{note.title | uppercase}}
            </router-link>

        </span>
            <button
                    class="button"
                    v-on:click="$emit('remove-note', note.id)"
            >&times;
            </button>

        </li>
        <div class="dropdown">
            <button class="btn" style="border-left:1px solid navy">
                &#8595;
            </button>
            <div class="dropdown-content">
                <p v-for="(t,index) of todo">{{index < 3 ? t.title : null}}</p>
            </div>
        </div>
    </div>
</template>

<script>
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

    .dropdown {
        position: absolute;
        display: inline-block;


        /* Dropdown Content (Hidden by Default) */
        &-content {
            display: none;
            position: absolute;
            background-color: #f1f1f1;
            min-width: 160px;
            z-index: 1;
        }

        /* Links inside the dropdown */
        &a {
            color: black;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
        }

        /* Change color of dropdown links on hover */
        &a:hover {
            background-color: #ddd
        }

        /* Show the dropdown menu on hover */
        &:hover .dropdown-content {
            display: block;
        }

        /* Change the background color of the dropdown button when the dropdown content is shown */
        .btn:hover, &:hover .btn {
            background-color: #0b7dda;
        }
    }
</style>