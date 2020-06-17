<template>
    <div>
        <button id="show-modal" @click="showModal = true">&times;</button>

        <div v-if="showModal" @close="showModal = false" v-on:blur="showModal = false" class="modal">
            <transition name="modal">
                <div class="modal-mask">
                    <div class="modal-wrapper">
                        <div class="modal-container">
                            <div class="modal-container-header">
                                <span>{{headerPhrase | uppercase}}</span>
                            </div>
                            <div class="modal-container-buttons">
                                <button
                                        v-on:click="showModal = false"
                                        class="cancel"
                                >{{'cancel' | uppercase}}
                                </button>
                                <button
                                        v-on:click="showModal = false; $emit('delete')"
                                        class="delete"
                                >{{'delete' | uppercase}}
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </transition>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ShowModal",
        props: ['headerPhrase'],
        data() {
            return {
                showModal: false
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
    #show-modal {
        border-radius: 10rem;
        border: none;
        font-weight: 600;
        font-size: 20px;
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

    .modal {
        &-mask {
            position: fixed;
            z-index: 9998;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: table;
            transition: opacity 0.3s ease;
        }

        &-wrapper {
            display: table-cell;
            vertical-align: middle;
        }

        &-container {
            width: 50%;
            margin: 0px auto;
            padding: 50px;
            background-color: #fff;
            border-radius: 2px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
            transition: all 0.3s ease;
            font-family: Helvetica, Arial, sans-serif;

            &-header {
                margin-bottom: 30px;

                & span {
                    font-size: 20px;
                }
            }

            &-buttons {
                display: flex;
                justify-content: space-evenly;

                & button {
                    font-size: 18px;
                    padding: 10px 20px;
                    outline: none;
                    border: none;
                    color: white;
                    cursor: pointer;
                    transition: background-color .1s ease;
                    border-radius: 2px;
                    position: relative;
                }

                &::before {
                    position: absolute;
                    width: 100%;
                    bottom: 0;
                    left: 0;
                    right: 0;
                    background: red;
                }

                & .cancel {
                    background: #228b22;
                    margin-right: 20px;

                    &:hover {
                        background: rgba(#228b22, .8);
                    }

                    &:active {
                        background: rgba(#228b22, .5);
                    }
                }

                & .delete {
                    background: #ff0000;

                    &:hover {
                        background: rgba(#ff0000, .6);
                    }

                    &:active {
                        background: rgba(#ff0000, .4);
                    }
                }
            }
        }
        &-enter {
            opacity: 0;
        }
        &-leave-active {
            opacity: 0;
        }
        &-enter &-container,
        &-leave-active &-container {
            -webkit-transform: scale(1.1);
            transform: scale(1.1);
        }
    }
</style>