<script setup lang="ts">
  import Trivia from './components/Trivia.vue';
  import { ref } from 'vue';
  import uniqueId from 'lodash.uniqueid';

  interface QuizDataItem {
    question: string;
    id: string;
    answers: { answer: string; answerId: string }[];
  }

  let quizData = ref<QuizDataItem[]>([]);

  interface ApiResponse {
    results: {
      correct_answer: string,
      incorrect_answers: string[],
      selected_answer: string,
      id: string,
      question: string
    }[];
  }

  const fetchedQuizData = async() => {
    const response = await fetch("https://opentdb.com/api.php?amount=5&type=multiple");
    const data: ApiResponse = await response.json();
    console.log(data);
    let remappedData = data.results.map(result=> {
      let allAnswers = [...result.incorrect_answers, result.correct_answer];
      let shuffledAnswers = shuffle(allAnswers);
      let decodedAnswers = shuffledAnswers.map(answer => {
        return htmlDecode(answer);
      })
      return {
        question: htmlDecode(result.question),
        id: uniqueId(),
        answers: decodedAnswers.map(x => {
          return {
            answer: x,
            answerId: uniqueId()
          }
        }),
        correct_answer: htmlDecode(result.correct_answer),
        selected_answer: "",
      }
    })
    quizData.value = remappedData;
  }

  function htmlDecode(input:string) {
        let doc = new DOMParser().parseFromString(input, "text/html");
        return doc.documentElement.textContent;
  }

  const shuffle = (array:string[]) => {
                for(let i = array.length - 1; i >= 1; i--) {
                    let j = Math.floor(Math.random() * (i + 1)); // 0 <= j <= i
                    let temp = array[j];
                    array[j] = array[i];
                    array[i] = temp;
                    }
                    return array;
                  }

  fetchedQuizData();
</script>

<template>
  <h1>Quizzical Vue3</h1>
  {{ quizData }}
  <Trivia
    v-for="data in quizData"
    :key="data.id"
    :question="data.question"
    :answers="data.answers"
  />
</template>

<style scoped>

</style>
