<template>
    <transition>
        <morpion v-if="show" />
    </transition>
</template>

<script>

export default {

    data() {
        return {
            show: null
        }
    },
}
</script>

<style>

</style>