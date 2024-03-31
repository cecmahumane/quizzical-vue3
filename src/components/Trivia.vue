<script setup lang="ts">
    import Buttons from './Buttons.vue';

    const props = defineProps({
        question: String,
        answers: Array
    })
</script>

<template>
    <p>{{ props.question }}</p>
    <Buttons
        v-for="answer in props.answers"
        :answer="answer"
        />
    <hr/>
</template>

<style scoped>

</style>
