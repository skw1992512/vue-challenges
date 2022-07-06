<script setup lang='ts'>
import {ref} from 'vue'
interface UseCounterOptions {
  min?: number
  max?: number
}

/**
 * 实现计数器函数,确保功能正常工作
 * 1. 加 (+)
 * 2. 减 (-)
 * 3. 重置 
 * 4. 最小值 & 最大值 选项支持
*/
function useCounter(initialValue = 0, options: UseCounterOptions = {}) {
  const count = ref(initialValue)
  const reset = () => count.value = initialValue
  const inc = ()=>{
    if(options.max && count.value >= options.max) return
    count.value++
  }
  const dec = ()=>{
    if((options.min || options.min === 0) && count.value <= options.min) return
    count.value--
  }
  return {
    count,
    inc,
    dec,
    reset
  }
}

const { count, inc, dec, reset } = useCounter(0, { min: 0, max: 10 })

</script>
<template>
  <div>
    <h1>{{ count }}</h1>
    <button @click="inc">+</button>
    <button @click="dec">-</button>
    <button @click="reset">reset</button>
  </div>
</template>