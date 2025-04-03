<script lang="ts" setup>
  import { ref } from 'vue'
  import Range from '@/components/range/Index.vue'
  import Smoke from '@/components/smoke/Index.vue'

  const range = ref(10)
</script>


<template>
  <main :class="M.layout">
    <header>
      <h1 :class="M.title">Smoke animation</h1>
    </header>
  
    <div :class="M.content">
      <Smoke :power="range" :start="range" />
      <Range v-model="range" />
      <div :class="M.label">Range of power</div>
    </div>
  
    <footer>
      <nav :class="M.nav">
        <a href="https://github.com/dterock/smoke-animation" target="_blank" :class="M.navLink">Source</a>
        <a href="https://github.com/dterock" target="_blank" :class="M.navLink">Github</a>
        <a href="https://hh.ru/resume/205c8ab0ff080e03f10039ed1f4f3946736d74" target="_blank" :class="M.navLink">Resume</a>
      </nav>
    </footer>
  </main>
</template>

<style module="M">
  .layout {
    display: grid;
    align-content: space-between;
    height: 100dvh;
    padding: 2rem;
  }

  .title {
    color: #fff;
    text-align: center;
  }

  .content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    color: #fff;
    text-transform: uppercase;
    font-size: .7rem;
    font-weight: bold;
    opacity: .7;
  }

  .nav {
    display: flex;
    justify-content: center;
    gap: 2rem;
  }

  .navLink {
    color: #fff;
    text-decoration: none;
  }

  .label {
    color: #fff;
    user-select: none;
  }
</style>