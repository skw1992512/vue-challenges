<script setup lang='ts'>

/**
 * 实现一个切换状态的可组合函数
 * 确保该功能正常工作
*/
import { ref } from 'vue'
function useToggle(flag:boolean) {
  const state = ref(flag)
  const toggle:any = () => {
    state.value = !state.value
  }
  return [state, toggle]
}

const [state, toggle] = useToggle(false)

</script>

<template>
  <p>State: {{ state ? 'ON' : 'OFF' }}</p>
  <p @click="toggle">
    Toggle state
  </p>
</template>