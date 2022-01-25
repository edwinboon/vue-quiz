<template>
  <div class="ctr">
    <questions 
      v-if="questionsAnswered < questions.length" 
      :questions="questions" 
      :questionsAnswered="questionsAnswered" 
      @question-answered="questionAnswered"
    />
    <results v-else />
    <button type="button" class="reset-btn">Reset</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { Question } from "./types/Question";
import { Result } from "./types/Result";
import Questions from "./components/Questions.vue";
import Results from "./components/Results.vue";

export default defineComponent({
  name: "App",
  components: { Questions, Results },
  setup() {
    let questionsAnswered = ref<number>(0)
    let totalCorrect = ref<number>(0)
    const questionAnswered = ref((is_correct: boolean): void=> {
      if(is_correct) {
        totalCorrect.value++
      }
      questionsAnswered.value++
    })

    // data for questions and results
    const questions = ref<Question[]>([
      {
        q: "What is 2 + 2?",
        answers: [
          {
            text: "4",
            is_correct: true,
          },
          {
            text: "3",
            is_correct: false,
          },
          {
            text: "Fish",
            is_correct: false,
          },
          {
            text: "5",
            is_correct: false,
          },
        ],
      },
      {
        q: 'How many letters are in the word "Banana"?',
        answers: [
          {
            text: "5",
            is_correct: false,
          },
          {
            text: "7",
            is_correct: false,
          },
          {
            text: "6",
            is_correct: true,
          },
          {
            text: "12",
            is_correct: false,
          },
        ],
      },
      {
        q: "Find the missing letter: C_ke",
        answers: [
          {
            text: "e",
            is_correct: false,
          },
          {
            text: "a",
            is_correct: true,
          },
          {
            text: "i",
            is_correct: false,
          },
        ],
      },
    ]);
    const result = ref<Result[]>([
      {
        min: 0,
        max: 2,
        title: "Try again!",
        desc: "Do a little more studying and you may succeed!",
      },
      {
        min: 3,
        max: 3,
        title: "Wow, you're a genius!",
        desc: "Studying has definitely paid off for you!",
      },
    ]);

    return { questionsAnswered, totalCorrect, questionAnswered, questions, result}
  },
});
</script>
