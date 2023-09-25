<template>
  <div class="container">
    <p class="display-3 pt-4 pb-2">🎈 GitHub Profile 마크다운 생성기</p>
    <CoverCard />
    <HitsCard />
    <GreetingsCard />
    <SkillCard />
    <TopLangsCard />
    <AlgorithmCard />
  </div>
</template>

<script setup>
import CoverCard from './components/CoverCard.vue';
import HitsCard from './components/HitsCard.vue';
import GreetingsCard from './components/GreetingsCard.vue'
import SkillCard from './components/SkillCard.vue';
import TopLangsCard from './components/TopLangsCard.vue';
import AlgorithmCard from './components/AlgorithmCard.vue';
</script>