<script lang="ts" setup>
  defineModel<number>({ default: 0 })
</script>


<template>
  <input
    @input="$emit('update:modelValue', +($event.target as HTMLInputElement).value)"
    type="range"
    :value="modelValue"
    :class="M.range"
    :style="`--v: ${modelValue}`"
  >
</template>


<style module="M">
  .range {
    appearance: none;
    outline: none;
    width: 100%;
    height: .15rem;
    background: linear-gradient(to right, #fff 0% calc(var(--v) * 1%), oklch(100% 0 0 / .25) calc(var(--v) * 1%) 100%);
    border-radius: .075rem;
  }

  .range::-webkit-slider-runnable-track {
    margin: 0 -1rem;
  }

  .range::-webkit-slider-thumb {
    appearance: none;
    background: transparent;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    background: #fff;
    cursor: e-resize;
    box-shadow: 0 .1rem .2rem oklch(.24 .0097 248.23 / .1),
                0 .2rem .4rem oklch(.24 .0097 248.23 / .1),
                0 .4rem .8rem oklch(.24 .0097 248.23 / .1);
  }
</style>