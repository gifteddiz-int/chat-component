<template>
  <div class="messages-list-wrapper" ref="messagesListWrapperRef">
    <div class="messages-list">
      <MessagesListItem :message="message" v-for="message in messages" :key="message.id"></MessagesListItem>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import MessagesListItem from "./MessagesListItem.vue";

const messagesListWrapperRef = ref(null);

defineProps({
  messages: {
    type: Array,
    required: true,
  },
});

const scrollMessagesToEnd = () => {
  if (messagesListWrapperRef.value) {
    messagesListWrapperRef.value.scrollTo({
      top: messagesListWrapperRef.value.scrollHeight,
      left: 0,
      behavior: "smooth",
    });
  }
};

defineExpose({ scrollMessagesToEnd });
</script>

<style scoped>
.messages-list-wrapper {
  padding: 8px 0;
  overflow-x: hidden;
  overflow-y: auto;
  height: 100%;
  scrollbar-width: thin;
  scrollbar-color: #ccc transparent;
}

.messages-list-wrapper::-webkit-scrollbar {
  width: 10px;
}

.messages-list-wrapper::-webkit-scrollbar-thumb {
  background-color: #ccc;
  border-radius: 6px;
}
.messages-list {
  display: flex;
  flex-direction: column;
  padding: 0 8px;
}
</style>
