<template>
    <h1>MORPION</h1>

    <button @click="show = !show" class="playBtn" v-if="!show">Play</button>
    <transition>
        <morpion v-if="show" />
    </transition>
    <img src="../../public/395930-wallpaper-synthwave-retrowave-grid-4k-hd.jpg" alt="" class="bg">
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
.v-enter-active,
.v-leave-active {
    transition: opacity 5s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}

h1 {
    animation: neon 1.5s ease-in-out infinite alternate;
}

.playBtn {
    padding: 10px 12px;
    margin: 4px;
    text-align: center;
    cursor: pointer;
    user-select: none;
    background-color: #42a4e4;
    box-shadow: inset -3px -3px #108de0;
    color: white;
    width: 200px;
    height: 50px;
    font-family: "Press Start 2P", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}

.playBtn:hover {
    background-color: #108de0;
    box-shadow: inset -4px -4px #006bb3;
    transform: translateY(-1px);
}

.bg {
    max-width: 100%;
    position: fixed;
    z-index: -1;
    animation: 120s linear 1s infinite alternate wallpaper;
}

@keyframes wallpaper {
    0% {
        transform: scale(1);
    }

    100% {
        transform: scale(2);
    }
}

@keyframes neon {
    0% {
        text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #fff, 0 0 40px #228dff, 0 0 70px #228dff, 0 0 80px #228dff, 0 0 100px #228dff, 0 0 150px #228dff;
    }

    100% {
        text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #fff, 0 0 20px #228dff, 0 0 35px #228dff, 0 0 40px #228dff, 0 0 50px #228dff, 0 0 75px #228dff;
    }
}
</style>