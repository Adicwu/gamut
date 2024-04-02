<template>
  <div class="app">
    <ul>
      <li v-for="item in finalGamutMap" :key="item.name">
        <span>{{ item.i }}</span>
        <span>{{ item.name }}</span>
        <span v-show="showSong">{{ item.song }}</span>
      </li>
    </ul>
    <div style="display: flex; gap: 20px">
      <button
        @click="start = Math.floor(Math.random() * (GamutMap.length - 0 + 1))"
      >
        RE
      </button>
      <button @click="reverse = !reverse">
        REVERSE {{ reverse ? "ON" : "OFF" }}
      </button>
      <button @click="showSong = !showSong">
        {{ !showSong ? "SHOW" : "HIDE" }}
      </button>
      <button
        @click="
          () => {
            reverse = false;
            start = 0;
          }
        "
      >
        RESET
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";

const GamutMap = [
  {
    name: "C",
    song: "do",
  },
  {
    name: "D",
    song: "re",
  },
  {
    name: "E",
    song: "mi",
  },
  {
    name: "F",
    song: "fa",
  },
  {
    name: "G",
    song: "sol",
  },
  {
    name: "A",
    song: "la",
  },
  {
    name: "B",
    song: "si",
  },
].map((item, i) => ({
  ...item,
  i: i + 1,
}));
const showSong = ref(false);
const start = ref(0);
const reverse = ref(false);

const finalGamutMap = computed(() => {
  const list = [...GamutMap];
  if (reverse.value) {
    list.reverse();
  }
  return [
    ...list.slice(start.value, list.length),
    ...list.slice(0, start.value),
  ];
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
  background-color: antiquewhite;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  ul {
    display: flex;
    list-style: none;
    font-size: 40px;
    gap: 30px;
    li {
      // width: 30px;
      display: flex;
      align-items: center;
      flex-direction: column;
    }
  }
  button {
    display: block;
    width: 160px;
    height: 40px;
    margin-top: 40px;
  }
}
</style>
