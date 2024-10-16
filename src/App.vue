<script setup lang="ts">
import { computed, ref } from "vue";

const image = ref<File | null>(null);
const imgInputRef = ref<HTMLInputElement | null>(null);

const imageSource = computed(() => {
  return image.value ? URL.createObjectURL(image.value) : undefined;
});

const inputChangeHandler = (e: Event) => {
  const target = e.target as HTMLInputElement;
  image.value = target.files?.[0] || null;
};

const inputClearHandler = () => {
  image.value = null;
  if (imgInputRef.value?.value) {
    imgInputRef.value.value = "";
  }
};
</script>

<template>
  <input
    type="file"
    ref="imgInputRef"
    accept="image/*"
    @change="inputChangeHandler"
  />

  <button v-if="image" @click="inputClearHandler">Clear Image</button>
  <img v-if="image" :src="imageSource" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
