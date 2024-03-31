<script setup lang="ts">
    import Buttons from './Buttons.vue';

    const props = defineProps({
        question: String,
        answers: Array
    })

    // const test: void = () => {
    //     alert(childEvent);
    // }
</script>

<template>
    <p>{{ props.question }}</p>
    <div class="btn-box">
        <Buttons
            v-for="answer in props.answers"
            :answer="answer"
            @click="test"
            />

    </div>
    <hr/>
</template>

<style scoped>
    .btn-box {
        display: flex;
        gap: 30px;

    }
</style>
