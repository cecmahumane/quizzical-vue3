<script setup lang="ts">
import { defineEmits } from "vue";
    const props = defineProps({
        answer: {
          type: Object,
        }
    })

    const emit = defineEmits(["childEvent"]);

    const childEvent = () => {
      emit(alert(props.answer?.answer))
    }

    
</script>

<template>
  <div @click="childEvent" class="btn">
    <p>{{ props.answer?.answer }}</p>
  </div>
</template>

<style scoped>
  .btn {
    border: 1px solid red;
    border-radius: 5px;
    padding: 5px 10px 5px;
    width: 100px;
    text-align: center;
  }
</style>
