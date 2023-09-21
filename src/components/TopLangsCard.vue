<template>
  <Card title="🚌 Top Langs">
    <div class="input-group">
      <InputLabel for="langs" label="username" />
      <TextInput id="langs-username" v-model="username" placeholder="GitHub에서 사용 중인 닉네임을 입력해주세요" />
      <InputLabel for="langs" label="layout" />
      <Dropdown id="langs-layout" v-model="layout" :items="layoutItems" />
    </div>
    <div style="text-align: right" class="py-3">
      <button class="btn btn-secondary mx-1" @click="langsGuide">
        가이드 보기
      </button>
      <button class="btn btn-primary" @click="langsUpdate">생성</button>
    </div>
    <Markdown v-if="modelValue" :key="'langs' + componentKey" :modelValue="modelValue" />
  </Card>
</template>

<script setup>
import { ref } from "vue";
import Markdown from "./Markdown.vue";
import Card from "./Card.vue";
import InputLabel from "./input/InputLabel.vue";
import TextInput from "./input/TextInput.vue";
import Dropdown from "./input/Dropdown.vue";

const layoutItems = [
  "none",
  "compact",
  "donut",
  "donut-vertical",
  "pie",
];

const username = ref('')
const layout = ref('')
const componentKey = ref(0);

const setParam = () => {
  const param = new URLSearchParams();
  param.set("username", username.value);
  if (layout.value != 'none') {
    param.set("layout", layout.value);
  }
  return param;
};

const modelValue = ref('');

const langsUpdate = () => {
  modelValue.value = ''
  modelValue.value += '### 🚌 Top Langs\n'
  modelValue.value += `![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?${setParam().toString()})`;
  componentKey.value++;
};

const langsGuide = () => {
  window.open("https://github.com/anuraghazra/github-readme-stats#top-languages-card", "_blank");
};
</script>
