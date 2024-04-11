<template>
  <div class="app">
    <b class="text-5xl">{{ FingerType[type] }} 指型</b>
    <p class="flex gap-4 mt-4 text-lg p-2 border-2 flex-wrap">
      <span v-for="(item, i) in cache" :key="i">{{ item }}</span>
    </p>

    <div class="mt-4 flex gap-4">
      <button @click="createCur">换一个</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import _ from "lodash";

const All = [
  "降3",
  "降4",
  "降5",
  "降6",
  "降7",
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  "升1",
  "升2",
  "升3",
  "升4",
  "升5",
  "升6",
  "升7",
  "升升1",
  "升升2",
  "升升3",
  "升升4",
];
const list = [
  All.slice(0, 17),
  All.slice(2, 18),
  All.slice(3, 20),
  All.slice(4, 21),
  All.slice(6, 24),
];
const FingerType = ["mi", "sol", "la", "xi", "re"];

const type = 0;
const cur = ref("");
const timer = ref("");
const cache = ref([]);

const random = (max, min = 0) => {
  return Math.floor(Math.random() * (max - min) + min);
};
const createCur = () => {
  cache.value = _.shuffle(list[type]);
};

createCur();
document.addEventListener("keydown", (e) => {
  if (e.keyCode === 32) {
    createCur();
  }
});
</script>
<style lang="less">
* {
  padding: 0;
  margin: 0;
}
.app {
  width: 100%;
  height: 100vh;
  background-color: #000;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #fff;
}
</style>
