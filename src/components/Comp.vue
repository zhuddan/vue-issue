<script setup lang="ts" generic="T extends Record<string, any>, R = T">
import type { Ref } from 'vue';
import { ref } from 'vue';
const props = defineProps<{
  fetch(): Promise<T[]>;
  formater?(item: T): R;
}>();

const list = ref([]) as Ref<R[]>;

function getData() {
  props.fetch().then((res) => {
    const formater = props.formater || (item => item as unknown as R);
    list.value = res.map(formater);
  });
}

getData();
</script>

<template>
  <ul>
    <slot :list="list"></slot>
  </ul>
</template>

<style scoped>

</style>