<script lang="ts" setup>
  import type { SmokeItem, SmokeProps } from './types'
  import { ref, onMounted, onUnmounted } from 'vue'

  const props = defineProps<SmokeProps>()
  const smoke = ref<SmokeItem[]>([])
  const speed = 100
  const limit = 50
  let timer: number

  function random(min: number, max: number) {
    return Math.floor(min + Math.random() * (max + 1 - min))
  }
  

  onMounted(() => {
    timer = setInterval(() => {
      smoke.value.push({
        id: Date.now(),
        offset: random(-50, 50),
        power: props.power,
        start: props.start
      })

      if (smoke.value.length > limit) {
        smoke.value.shift()
      }
    }, speed)
  })

  onUnmounted(() => clearInterval(timer))
</script>


<template>
  <div :class="M.container">
    <span
      v-for="item in smoke"
      :key="item.id"
      :class="M.smoke"
      :style="{'--_p': item.power, '--_s': item.start, '--_o': item.offset}"
    />
  </div>
</template>


<style module="M">
  @property --_trX {
    syntax: "<percentage>";
    initial-value: -50%;
    inherits: false;
  }

  @property --_trY {
    syntax: "<percentage>";
    initial-value: -400%;
    inherits: false;
  }

  @keyframes anim {
    0% {
      --_trY: -65%;
      scale: .5;
    }
    10%, 100% {
      --_trX: calc((var(--_o) - 50) * 1%);
      scale: 1;
    }
    80%, 100% {
      scale: 0;
    }
  }

  .container {
    position: relative;
    width: 100%;
  }

  .smoke {
    position: absolute;
    display: inline-block;
    width: clamp(.5rem, var(--_p) * .1rem, 6rem);
    aspect-ratio: 1/1;
    background: #fff;
    border-radius: 50%;
    left: calc(var(--_s) * 1%);
    translate: var(--_trX) var(--_trY);
    z-index: -1;
    animation: anim calc(v-bind(speed) * v-bind(limit) * 1ms) ease-out forwards;
    box-shadow: 0 .1rem .2rem oklch(.24 .0097 248.23 / .1),
                0 .2rem .4rem oklch(.24 .0097 248.23 / .1),
                0 .4rem .8rem oklch(.24 .0097 248.23 / .1);
  }
</style>