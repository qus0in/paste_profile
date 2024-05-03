<template>
  <Card title="🦾 Skills">
    <div class="input-group">
      <InputLabel for="skills" label="name" />
      <input class="form-control" list="datalistOptions" id="skills-name" v-model="skillsName">
      <datalist id="datalistOptions">
        <option v-for="icon in icons" :key="icon.title" :value="icon.title"  />
      </datalist>
    </div>
    <div class="mt-3 input-group d-flex justify-content-end">
      <button class="btn btn-outline-secondary" type="button"
        @click="addGroup1"
      ><code>Lang and Frameworks</code>에 추가</button>
      <button class="btn btn-outline-secondary" type="button"
        @click="addGroup2"
      ><code>Infra and Tools</code>에 추가</button>
    </div>
    <div class="mt-3">
      <p class="mb-1 fw-bold">🧑‍💻 Lang and Frameworks</p>
      <div class="d-flex flex-wrap">
        <button v-for="g1 in group1" :key="g1 + '_g1'" class="btn m-0 p-1" @click="skillsRemove1(g1)">
          <img :src=nameToInfo(g1)>
        </button>
      </div>
    </div>
    <div class="mt-3">
      <p class="mb-1 fw-bold">🛠️ Infra and Tools</p>
      <div class="d-flex flex-wrap">
        <button v-for="g2 in group2" :key="g2 + '_g2'" class="btn m-0 p-1" @click="skillsRemove2(g2)">
          <img :src=nameToInfo(g2)>
        </button>
      </div>
    </div>

    <div style="text-align: right" class="py-3">
      <button class="btn btn-secondary me-1" @click="skillsGuide1">
        가이드 보기 (뱃지)
      </button>
      <button class="btn btn-secondary me-1" @click="skillsGuide2">
        가이드 보기 (아이콘)
      </button>
      <button class="btn btn-primary" @click="skiilsUpdate">생성</button>
    </div>
    <Markdown v-if="modelValue" :key="'skills' + componentKey" :modelValue="modelValue" />
  </Card>
</template>

<script setup>
import { ref } from "vue";
import Markdown from "./Markdown.vue";
import Card from "./Card.vue";
import InputLabel from "./input/InputLabel.vue";
import * as icons from 'simple-icons';

const componentKey = ref(0);
const modelValue = ref('');
const skillsName = ref('')
const group1 = ref(new Set())
const group2 = ref(new Set())

const addGroup1 = () => {
  group1.value.add(skillsName.value)
  skillsName.value = ''
}
const addGroup2 = () => {
  group2.value.add(skillsName.value)
  skillsName.value = ''
}
const nameToInfo = (name) => {
  const n1 = name.replace('.', 'dot').replace(' ', '').replace('-', '')
  const n2 = n1.charAt(0).toUpperCase() + n1.slice(1).toLowerCase()
  const icon = icons['si' + n2]
  if (!icon) return `https://img.shields.io/badge/${n2}-000000.svg?&style=for-the-badge`
  return `https://img.shields.io/badge/${icon.slug}-${icon.hex}.svg?&style=for-the-badge&logo=${icon.slug}&logoColor=white`
}
const skillsRemove1 = (name) => {
  group1.value.delete(name)
}
const skillsRemove2 = (name) => {
  group2.value.delete(name)
}
const skiilsUpdate = () => {
  modelValue.value = ''
  modelValue.value += '### 🦾 Skills\n';
  modelValue.value += '**🧑‍💻 Lang and Frameworks**\n';
  for (const g1 of group1.value) {
    modelValue.value += `![${g1}](${nameToInfo(g1)}) `
  }
  modelValue.value += '\n\n'
  modelValue.value += '**🛠️ Infra and Tools**\n';
  for (const g2 of group2.value) {
    modelValue.value += `![${g2}](${nameToInfo(g2)}) `
  }
  componentKey.value++;
};
const skillsGuide1 = () => {
  window.open("https://shields.io/badges", "_blank");
};
const skillsGuide2 = () => {
  window.open("https://simpleicons.org/", "_blank");
};
</script>
