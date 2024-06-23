<script setup>

    import { ref } from 'vue';

    const questions = ref([
    {
    question: "¿Cuál es el color del cielo?",
    answers: [
      { name: "Azul", correct: true },
      { name: "Rojo", correct: false },
      { name: "Verde", correct: false },
      { name: "Amarillo", correct: false }
    ]
    },
    {
    question: "¿Cuál es el color de la hierba?",
    answers: [
      { name: "Azul", correct: false },
      { name: "Rojo", correct: false },
      { name: "Verde", correct: true },
      { name: "Amarillo", correct: false }
    ]
    }
    ]);

    const boxState = ref(false);
    const currentQuestionIndex = ref(0);
    const selectedAnswerIndex = ref(null);


    const verifyAnswer = (correct) => {
      boxState.value = correct;
    };

    const selectAnswer = (index, correct) => {
      selectedAnswerIndex.value = index;
      verifyAnswer(correct);
    };

    const handleNextQuestion = () => {
      if (currentQuestionIndex.value < questions.value.length - 1) {
        currentQuestionIndex.value++;
        boxState.value = null;
        selectedAnswerIndex.value = null;
      } else {
        // Logic to handle end of questions can be added here if needed
      }
    };


</script>

<template>
    <div class="max-w-6xl w-full mx-auto flex flex-col justify-center items-center">
    <div :class="boxState === true ? 'bg-green-500' : boxState === false ? 'bg-red-500' : 'bg-gray-500'" class="rounded-md px-7 py-14 w-2/5 text-center mt-10">
      <h1>UFPSO</h1>
    </div>

    <div v-if="currentQuestionIndex < questions.length" class="p-3 flex flex-col justify-center items-center">
      <h1 class="text-xl font-bold mb-4">{{ questions[currentQuestionIndex].question }}</h1>
      <div class="grid grid-cols-2 gap-4 w-full">
        <div
          v-for="(answer, index) in questions[currentQuestionIndex].answers"
          :key="index"
          class="p-4 border cursor-pointer text-center w-full h-24"
          :class="{
            'bg-red-400': selectedAnswerIndex === index && !answer.correct,
            'bg-green-400': selectedAnswerIndex === index && answer.correct,
            'bg-red-600 hover:bg-red-900': index === 0,
            'bg-blue-600 hover:bg-blue-950': index === 1,
            'bg-yellow-400 hover:bg-yellow-700': index === 2,
            'bg-green-600 hover:bg-green-800': index === 3,
          }"
          @click="selectAnswer(index, answer.correct)"
        >
          {{ answer.name }}
        </div>
      </div>
    </div>

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
    <br><br><br>
  </div>


</template>