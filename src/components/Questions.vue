<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar"></div>
      <div class="status">1 out of 3 questions answered</div>
    </div>
    <div class="single-question" v-for="question in questions" :key="question.q">
      <div class="question">{{ question.q }}</div>
      <div class="answers" v-for="answer in question.answers" :key="answer.text">
        <div class="answer">{{  answer.text }}</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType} from 'vue'
import { Question } from '@/types/Question'

export default defineComponent({
  name: 'questions',
  props: {
    /**
     * Questions: the questions a user can answer
     */
    questions: {
      required: true,
      type: Array as PropType<Question[]>
    }
  }
})
</script>
