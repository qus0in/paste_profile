<template>
  <Card title="👋 인사말">
    <div class="input-group">
      <InputLabel for="cover" label="kwd" />
      <TextInput id="cover-kwd" v-model="kwd" placeholder="본인을 설명하는 키워드를 입력해주세요" />
    </div>
    <div style="text-align: right" class="py-3">
      <button class="btn btn-primary" :disabled="isLoading" @click="greetingsUpdate">생성</button>
    </div>
    <div class="d-flex justify-content-center">
      <div v-if="isLoading" class="spinner-border" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
    </div>

    <Markdown v-if="modelValue && !isLoading" :key="'greetings' + componentKey" :modelValue="modelValue" />
  </Card>
</template>

<script setup>
import { ref } from "vue";
import Markdown from "./Markdown.vue";
import Card from "./Card.vue";
import InputLabel from "./input/InputLabel.vue";
import TextInput from "./input/TextInput.vue";
import axios from 'axios';
const kwd = ref("");
const componentKey = ref(0);
const isLoading = ref(false);

const modelValue = ref('');

const greetingsUpdate = async () => {
  const URL = 'https://5er4vmpce5nm35zzw7gco2u74i0lzpag.lambda-url.ap-northeast-2.on.aws/'
  isLoading.value = true;
  try {
    const res = await axios.post(URL, {
      'kwd': kwd.value
    }, {withCredentials: true})
    modelValue.value = res.data.message;
    componentKey.value++;
  } catch (err) {
    console.error(err)
  } 
  isLoading.value = false;
};

</script>
