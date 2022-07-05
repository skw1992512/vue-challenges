<script setup lang='ts'>
import { ref,watch } from "vue"

const count = ref(0)

/**
 * 实现`until`函数
*/

function until(initial:any) {
  function toBe(value:any) {
    return new Promise<void>((resolve, reject) => {
      const stop = watch(initial, (newValue:any) => {
      if(newValue === value) {
        resolve(newValue)
        stop()
      }
    })
    })
  }

  return {
    toBe,
  }
}

async function increase() {
  count.value = 0
  setInterval(() => {
    count.value++
  }, 1000)
  await until(count).toBe(3)
  console.log(count.value === 3) // 确保输出为true
}

</script>

<template>
 <p @click="increase"> 
   Increase {{count}}
 </p>
</template>
