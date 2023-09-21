<template>
  <Card title="🚩 Algorithm Ranking">
    <div class="input-group">
      <InputLabel for="algo" label="username" />
      <TextInput id="algo-username" v-model="username" placeholder="BOJ에서 사용 중인 닉네임을 입력해주세요" />
      <InputLabel for="algo" label="version" />
      <Dropdown id="algo-version" v-model="version" :items="versionItems" />
    </div>
    <div style="text-align: right" class="py-3">
      <button class="btn btn-secondary mx-1" @click="algoGuide">
        가이드 보기
      </button>
      <button class="btn btn-primary" @click="algoUpdate">생성</button>
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

const versionItems = [
  "V1",
  "V2",
  "MINI",
];

const username = ref('')
const version = ref('V2')
const componentKey = ref(0);

const setParam = () => {
  const param = new URLSearchParams();
  param.set("boj", username.value);
  return param;
};

const modelValue = ref('');

const algoUpdate = () => {
  modelValue.value = ''
  modelValue.value += '### 🚩 Algorithm Ranking\n'
  let api;
  switch (version.value) {
    case 'MINI':
      api = 'api/mini'
      break
    case 'V2':
      api = 'api/v2'
      break
    case 'V1':
      api = 'api'
      break
  }
  const URL = `https://mazassumnida.wtf/${api}/generate_badge?${setParam().toString()}`
  modelValue.value += `[![Algorithm Ranking](${URL})](https://solved.ac/profile/${username.value})`;
  componentKey.value++;
};

const algoGuide = () => {
  window.open("https://github.com/mazassumnida/mazassumnida", "_blank");
};
</script>
