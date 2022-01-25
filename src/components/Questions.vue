<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div class="single-question" v-for="(question, index) in questions" :key="question.q" v-show="questionsAnswered === index">
        <div class="question">{{ question.q }}</div>
        <div class="answers" v-for="answer in question.answers" :key="answer.text">
          <div class="answer" @click.prevent="selectAnswer(answer.is_correct)">{{  answer.text }}</div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { defineComponent, defineEmits, PropType, ref} from 'vue'
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
    },
    /**
     * QuestionsAnswered: Keep track of the questions answered
     */
    questionsAnswered: {
      required: true,
      type: Number
    }
  },
  setup(props, context) {
    // define emits
    const emit = defineEmits<{
      (event: 'question-answered', is_correct: boolean): void
    }>()

    // define selectAnswer
    const selectAnswer = ref((is_correct: boolean) => {
      context.emit('question-answered', is_correct)
    })

    return { selectAnswer, emit }
  }
})
</script>
