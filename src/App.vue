<script setup lang="ts">
import Dialog from '@/components/Dialog.vue';
import { ref } from 'vue';
const showDialog = ref(false);
</script>

<template>
  <main>
    <Dialog 
      v-model="showDialog"
      title="提示"
      content="这是一个对话框"
     />
     <button @click="showDialog = true">展示弹窗</button>
  </main>
</template>

<style>
body {
  margin: 0;
}
</style>
