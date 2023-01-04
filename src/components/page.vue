<template>
    <form action="" class="form">
        <input type="text" :v-bind="player1">
        <input type="text" :v-bind="player2">
    </form>
    <button @click="show = !show" class="playBtn"  v-if="!show">Play</button>
    <transition>
        <morpion v-if="show" />
    </transition>
</template>

<script>
import morpion from './morpion.vue'

export default {
    components: {
        morpion
    },

    data() {
        return {
            show: null
        }
    },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Press+Start+2P');


.v-enter-active,
.v-leave-active {
    transition: opacity 5s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}

.playBtn {
    padding: 10px 12px;
    margin: 4px;
    font-family: "Press Start 2P", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
    text-align: center;
    cursor: pointer;
    user-select: none;
    background-color: #42a4e4;
    box-shadow: inset -3px -3px #108de0;
    color: white;
    width: 200px;
    height: 50px;
}

.playBtn:hover {
    background-color: #108de0;
    box-shadow: inset -4px -4px #006bb3;
    transform: translateY(-1px);
}

.playBtn:focus {}
</style>