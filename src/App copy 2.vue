<template>
  <div class="app">
    <b class="text-5xl">{{ cur }}</b>
    <p class="flex gap-4 mt-4 text-lg p-2 border-2 flex-wrap">
      <span v-for="(item, i) in cache" :key="i">{{ item }}</span>
    </p>

    <div class="mt-4 flex gap-4">
      <button @click="cache.splice(0)">清空缓存</button>
      <button @click="createCur">换一个</button>
      <button @click="startCreateCur">随机{{ timer ? "停止" : "开始" }}</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const list = [
  [
    "升3",
    "升4",
    null,
    "升5",
    null,
    "升6",
    null,
    "升7",
    "升升1",
    null,
    "升升2",
    null,
    "升升3",
    "升升4",
  ],
  [
    "7",
    "升1",
    null,
    "升2",
    null,
    "升3",
    "升4",
    null,
    "升6",
    null,
    "升7",
    "升升1",
  ],
  [
    "5",
    null,
    "6",
    null,
    "7",
    "升1",
    null,
    "升2",
    null,
    "升3",
    "升4",
    null,
    "升5",
  ],
  ["2", null, "3", "4", null, "5", null, "6", null, "7", "升1", null, "升2"],
  ["降6", null, "降7", "1", null, "2", null, "3", "4", null, "5", null, "6"],
  [
    "降3",
    "降4",
    null,
    "降5",
    null,
    "降6",
    null,
    "降7",
    "1",
    null,
    "2",
    null,
    "3",
    "4",
  ],
];

const cur = ref("");
const timer = ref("");
const cache = ref([]);

const random = (max, min = 0) => {
  return Math.floor(Math.random() * (max - min) + min);
};
const createCur = () => {
  const n = random(1, 5);
  const x = list[n];
  let res = null;
  while (!res) {
    res = x[random(x.length)];
  }
  cur.value = `${n + 1}弦-${res}`;
  cache.value.push(cur.value);
};
const startCreateCur = () => {
  if (timer.value) {
    clearInterval(timer.value);
    timer.value = null;
  } else {
    timer.value = setInterval(() => {
      createCur();
    }, 6000);
  }
};

// startCreateCur();
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
