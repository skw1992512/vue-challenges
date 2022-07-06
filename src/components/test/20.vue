<script setup lang="ts">
/**
 * 实现以下自定义指令
 * 确保在一定时间内当快速点击按钮多次时只触发一次点击事件
 * 你需要支持节流延迟时间选项, 用法如 `v-debounce-click:ms`
 *
 */
import { Directive } from "vue";
const debounce = (handler: Function, daley: number = 200) => {
  let timer: number | null = null;
  return (...args: any[]) => {
    clearTimeout(timer!);
    timer = setTimeout(() => {
      timer = null;
      handler.apply(args);
    }, daley);
  };
};

const useVDebounceClick = (): Directive => {
  let handler: {
    (...args: any[]): void;
    (this: HTMLElement, ev: MouseEvent): any;
    (this: HTMLElement, ev: MouseEvent): any;
  } | null = null;
  return {
    mounted(el, binding) {
      handler = debounce(binding.value, Number.parseInt(<string>binding.arg));
      el.addEventListener("click", handler);
    },
    unmounted(el) {
      handler && el.removeEventListener("click", handler);
      handler = null;
    },
  };
};

const VDebounceClick = useVDebounceClick();

function onClick() {
  console.log("Only triggered once when clicked many times quicky");
}
</script>

<template>
  <button v-debounce-click:200="onClick">Click on it many times quickly</button>
</template>
