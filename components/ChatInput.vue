<script setup>
import { ref } from 'vue';

const store = useChatStore();
const chatInput = ref('');

const handleNewMessage = () => {
  if (!chatInput.value.trim()) return;
  store.sendMessage(chatInput.value);
  chatInput.value = '';
};
</script>

<template>
  <div class="flex justify-between gap-4 max-h-32">
    <div class="w-full">
      <UTextarea class="w-full"
                 autoresize
                 autofocus
                 :rows="1"
                 :maxrows="5"
                 color="primary"
                 variant="outline"
                 v-model="chatInput"
                 placeholder="🦙 Ask Llama anything..."
                 @keydown="(e) => {
                  if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    handleNewMessage();
                  }
                }"
                 :ui="{
                  base: 'resize-none bg-(--ui-bg-elevated)/50'
                }" />
    </div>
    <div class="mt-auto">
      <UButton icon="i-heroicons-paper-airplane"
               size="md"
               color="primary"
               variant="subtle"
               :disabled="!chatInput"
               @click="handleNewMessage" />
    </div>
  </div>
</template>