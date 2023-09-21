<template>
  <Card title="📈 방문자수 카운터">
    <div class="input-group">
      <InputLabel for="hits" label="username" />
      <TextInput id="hits-username" v-model="username" />
      <InputLabel for="hits" label="border" />
      <Dropdown id="hits-border" v-model="border" :items="borderItems" />
      <InputLabel for="hits" label="title" />
      <TextInput id="hits-title" v-model="title" />
    </div>
    <div style="text-align: right" class="py-3">
      <button class="btn btn-secondary mx-1" @click="hitsGuide">
        가이드 보기
      </button>
      <button class="btn btn-primary" @click="hitsUpdate">생성</button>
    </div>
    <Markdown v-if="modelValue" :key="'hits' + componentKey" :modelValue="modelValue" />
  </Card>
</template>

<script setup>
import { ref } from "vue";
import Markdown from "./Markdown.vue";
import Card from "./Card.vue";
import InputLabel from "./input/InputLabel.vue";
import TextInput from "./input/TextInput.vue";
import Dropdown from "./input/Dropdown.vue";

const borderItems = ["FLAT", "ROUND"];

const username = ref("");
const border = ref("ROUND");
const title = ref("hits");
const componentKey = ref(0);

const setParam = () => {
  const param = new URLSearchParams();
  param.set("url", "https://github.com/" + username.value);
  param.set("edge_flat", border.value == 'FLAT')
  param.set("title", title.value)
  return param;
};

const modelValue = ref('');

const hitsUpdate = () => {
  modelValue.value = `![hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?${setParam().toString()})`;
  componentKey.value++;
};

const hitsGuide = () => {
  window.open("https://hits.seeyoufarm.com/", "_blank");
};
</script>
