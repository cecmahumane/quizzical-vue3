<script setup lang="ts">
import { defineEmits, ref, inject } from "vue";
    const props = defineProps({
        answer: {
          type: Object,
        }
    })

    const buttonColour = ref('blue');
    var isToggled: boolean = true

    const changeColour = () => {
      isToggled = !isToggled;
      buttonColour.value = isToggled ? 'blue' : 'red';
    }

    const emit = defineEmits(["childEvent"]);

    const childEvent = () => {
      // emit(alert(props.answer?.answer))
      changeColour();
    }

    const emittedData = inject('sharedData');
</script>
<template>
  <div @click="childEvent" class="btn" :style="{backgroundColor: buttonColour}">
    <p>{{ props.answer?.answer }}</p>
  </div>
  <p>{{ emittedData }}</p>
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
