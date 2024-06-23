<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps({  //propiedad que el componente va a recibir del padre (MainKahoot)
  question: Object,  //creo un objeto 
});

const selectedAnswerIndex = ref(null); //el ref(null) es para rastrear la respuesta seleccionada por el usuario
const emits = defineEmits(['verifyAnswer']); //defineEmits para eventos personalizados

function selectAnswer(index, correct) { 
  selectedAnswerIndex.value = index;
  emits('verifyAnswer', correct); //emitir el evento mandando como parametro al correct que es un valor boolano (definido en el json)
}

</script>

<template>
  <div class="p-3 flex flex-col justify-center items-center">
    <h1 class="text-xl font-bold mb-4">{{ question.question }}</h1>
    <div class="grid grid-cols-2 gap-4 w-full">
      <div
        v-for="(answer, index) in question.answers"
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
</template>
