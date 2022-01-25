<template>
  <div class="result">
    <div class="title">{{ result[resultIndex].title }}</div>
    <div class="desc">{{ result[resultIndex].desc }}</div>
  </div>  
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import { Result } from '@/types/Result'

export default defineComponent({
  name: 'results',
  props: {
    /**
     * Result: the quiz result
     */
    result: {
      required: true,
      type: Array as PropType<Result[]>
    },
    /**
     * TotalCorrect: Total of correct answered questions
     */
    totalCorrect: {
      required: true,
      type: Number 
    },
  },
  setup(props) {
    const resultIndex = computed(() => {
      let index = 0

      props.result.forEach((e: Result, i: number) => {
        if(e.min <= props.totalCorrect && e.max >= props.totalCorrect) {
          index = i;
        }
      })

      return index
    })

    return { resultIndex }
  }
})
</script>
