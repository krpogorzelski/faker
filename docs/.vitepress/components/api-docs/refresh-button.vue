<script setup lang="ts">
import { ref } from 'vue';

const { refresh } = defineProps<{ refresh: () => Promise<void> }>();

const spinning = ref(false);

async function onRefresh() {
  spinning.value = true;
  await refresh();
  spinning.value = false;
}
</script>

<template>
  <button class="refresh" @click="onRefresh">
    <div :class="{ spinning: spinning }">⟳</div>
  </button>
</template>

<style scoped>
button.refresh {
  border: 1px solid var(--vp-code-copy-code-border-color);
  border-radius: 4px;
  width: 40px;
  height: 40px;
  font-size: 25px;
  vertical-align: middle;
}

button.refresh:hover {
  background-color: var(--vp-code-copy-code-bg);
  opacity: 1;
}

.spinning {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
