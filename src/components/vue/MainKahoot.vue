<script setup>
import { ref } from 'vue';
import KahootQuestion from './KahootQuestion.vue';
import content from '../content.json';

const questions = ref(content[0].questions);
const currentQuestionIndex = ref(0);
const boxState = ref(null);

function handleNextQuestion() {
  if (currentQuestionIndex.value < questions.value.length - 1) {
    currentQuestionIndex.value++;
    resetBoxState();
  } else {
    console.log('Cuestionario completado');
  }
}

function verifyAnswer(isCorrect) {
  boxState.value = isCorrect;
}

function resetBoxState() {
  boxState.value = null;
}

</script>

<template>
  <div class="max-w-6xl w-full mx-auto flex flex-col justify-center items-center">
    <div :class="boxState === true ? 'bg-green-500' : boxState === false ? 'bg-red-500' : 'bg-gray-500'" class="rounded-md px-7 py-14 w-2/5 text-center mt-10">
      <h1>UFPSO</h1>
    </div>

    <KahootQuestion
      v-if="currentQuestionIndex < questions.length"
      :question="questions[currentQuestionIndex]"
      @verifyAnswer="verifyAnswer"
    />

    <div v-else>
      <h2 class="text-xl font-bold">¡Has terminado el cuestionario!</h2>
    </div>

    <button
      v-if="boxState !== null"
      @click="handleNextQuestion"
      class="py-2 px-4 mt-4 bg-teal-400 text-white rounded-md"
    >
      Siguiente
    </button>
  </div>
</template>
