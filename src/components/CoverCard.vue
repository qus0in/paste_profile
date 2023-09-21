<template>
  <Card title="🌊 커버 (Capsule-render)">
    <div class="input-group">
      <InputLabel for="cover" label="type" />
      <Dropdown id="cover-type" v-model="coverType" :items="typeItems" />
      <InputLabel for="cover" label="color" />
      <Dropdown id="cover-color" v-model="color" :items="colorItems" />
      <InputLabel for="cover" label="height" />
      <NumberInput id="cover-height" v-model="height" />
    </div>
    <div class="input-group">
      <InputLabel for="cover" label="text" />
      <TextInput id="cover-text" v-model="text" />
    </div>
    <div class="input-group">
      <InputLabel for="cover" label="desc" />
      <TextInput id="cover-desc" v-model="desc" />
    </div>
    <div class="input-group">
      <InputLabel for="cover" label="fontSize" />
      <NumberInput id="cover-fontSize" v-model="fontSize" />
      <InputLabel for="cover" label="fontAlign" />
      <NumberInput id="cover-fontAlign" v-model="fontAlign" />
      <InputLabel for="cover" label="fontAlignY" />
      <NumberInput id="cover-fontAlignY" v-model="fontAlignY" />
    </div>
    <div class="input-group">
      <InputLabel for="cover" label="descSize" />
      <NumberInput id="cover-descSize" v-model="descSize" />
      <InputLabel for="cover" label="descAlign" />
      <NumberInput id="cover-descAlign" v-model="descAlign" />
      <InputLabel for="cover" label="descAlignY" />
      <NumberInput id="cover-descAlignY" v-model="descAlignY" />
    </div>
    <div style="text-align: right" class="py-3">
      <button class="btn btn-secondary mx-1" @click="coverGuide">
        가이드 보기
      </button>
      <button class="btn btn-primary" @click="coverUpdate">생성</button>
    </div>
    <Markdown v-if="modelValue" :key="componentKey" :modelValue="modelValue" />
  </Card>
</template>

<script setup>
import { ref } from "vue";
import Markdown from "./Markdown.vue";
import Card from "./Card.vue";
import InputLabel from "./input/InputLabel.vue";
import TextInput from "./input/TextInput.vue";
import Dropdown from "./input/Dropdown.vue";
import NumberInput from "./input/NumberInput.vue";

const typeItems = [
  "wave",
  "rect",
  "soft",
  "rounded",
  "cylinder",
  "waving",
  "transparent",
];
const colorItems = ["auto", "gradient"];

const coverType = ref("waving");
const height = ref(360);
const componentKey = ref(0);
const text = ref("Hello World!");
const color = ref("auto");
const desc = ref("Happy Coding Day");
const fontSize = ref(70);
const fontAlign = ref(50);
const fontAlignY = ref(50);
const descSize = ref(20);
const descAlign = ref(50);
const descAlignY = ref(60);

const setParam = () => {
  const param = new URLSearchParams();
  param.set("type", coverType.value);
  param.set("color", color.value);
  param.set("height", height.value);
  param.set("text", text.value);
  param.set("fontSize", fontSize.value);
  param.set("fontAlign", fontAlign.value);
  param.set("fontAlignY", fontAlignY.value);
  param.set("desc", desc.value);
  param.set("descSize", descSize.value);
  param.set("descAlign", descAlign.value);
  param.set("descAlignY", descAlignY.value);
  return param;
};

const modelValue = ref('');

const coverUpdate = () => {
  modelValue.value = `![header](https://capsule-render.vercel.app/api?${setParam().toString()})`;
  componentKey.value++;
};

const coverGuide = () => {
  window.open("https://github.com/kyechan99/capsule-render", "_blank");
};
</script>
