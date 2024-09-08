<template>
  <div class="chat-item">
    <div class="header">
      <button class="header-back" @click="emits('selectChat', null)">
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M11.7071 4.29289C12.0976 4.68342 12.0976 5.31658 11.7071 5.70711L6.41421 11H20C20.5523 11 21 11.4477 21 12C21 12.5523 20.5523 13 20 13H6.41421L11.7071 18.2929C12.0976 18.6834 12.0976 19.3166 11.7071 19.7071C11.3166 20.0976 10.6834 20.0976 10.2929 19.7071L3.29289 12.7071C3.10536 12.5196 3 12.2652 3 12C3 11.7348 3.10536 11.4804 3.29289 11.2929L10.2929 4.29289C10.6834 3.90237 11.3166 3.90237 11.7071 4.29289Z" fill="#000000" />
        </svg>
      </button>
      <div class="header-img">
        <img :src="currentChat.img" alt="" />
      </div>
      <div class="header-title">{{ currentChat.title }}</div>
    </div>
    <MessagesList :messages="messages" ref="messagesListRef" />
    <MessageInput @send-message="handleSend" />
  </div>
</template>
<script setup>
import { nextTick, onMounted, ref } from "vue";
import MessageInput from "./MessageInput.vue";
import MessagesList from "./MessagesList.vue";

defineProps({
  currentChat: {
    type: Object,
    required: true,
  },
});

const emits = defineEmits("selectChat");

const messagesListRef = ref(null);

const handleSend = (message) => {
  messages.value.push({
    id: new Date().getTime(),
    sender: "user",
    time: new Date().toLocaleTimeString(),
    text: message,
  });
  nextTick(() => {
    if (messagesListRef.value) {
      messagesListRef.value.scrollMessagesToEnd();
    }
  });
};

onMounted(() => {
  if (messagesListRef.value) {
    messagesListRef.value.scrollMessagesToEnd();
  }
});

const messages = ref([
  {
    id: 1,
    sender: "user",
    time: "12:00:31",
    text: "Сообщение от пользователя. Как пример на пару предложений, визуально примерно средняя длина сообщения",
  },
  {
    id: 2,
    sender: "admin",
    time: "13:12:12",
    text: "Модератор ответил на сообщение. Другой пример средняя длина сообщения",
  },
  {
    id: 3,
    sender: "user",
    time: "13:15:12",
    text: "Сообщение от пользователя. Как пример на пару предложений, визуально примерно средняя длина сообщения",
  },
  {
    id: 4,
    sender: "admin",
    time: "13:16:12",
    text: "Модератор ответил на сообщение. Другой пример средняя длина сообщения",
  },
  {
    id: 5,
    sender: "user",
    time: "13:17:12",
    text: "Сообщение от пользователя. Как пример на пару предложений, визуально примерно средняя длина сообщения",
  },
  {
    id: 6,
    sender: "admin",
    time: "13:18:12",
    text: "Модератор ответил на сообщение. Другой пример средняя длина сообщения",
  },
  {
    id: 7,
    sender: "user",
    time: "13:19:12",
    text: "Сообщение от пользователя. Как пример на пару предложений, визуально примерно средняя длина сообщения",
  },
  {
    id: 8,
    sender: "admin",
    time: "13:20:12",
    text: "Модератор ответил на сообщение. Другой пример средняя длина сообщения",
  },
  {
    id: 9,
    sender: "user",
    time: "13:21:12",
    text: "Сообщение от пользователя. Как пример на пару предложений, визуально примерно средняя длина сообщения",
  },
]);
</script>

<style scoped>
.chat-item {
  height: 100%;
  display: flex;
  flex-direction: column;
}
.header {
  display: flex;
  align-items: center;
  padding: 10px;
  background-color: #fff;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.01), 0 2px 2px rgba(0, 0, 0, 0.01), 0 4px 4px rgba(0, 0, 0, 0.01), 0 8px 8px rgba(0, 0, 0, 0.01), 0 16px 16px rgba(0, 0, 0, 0.01);
  position: relative;
  z-index: 5;
}
.header-back {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 0;
  width: 40px;
  height: 40px;
  border: 0;
  background-color: transparent;
  cursor: pointer;
  flex-shrink: 0;
}
.header-back svg {
  width: 21px;
  height: 21px;
  fill: #000000;
}
.header-img {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  overflow: hidden;
  flex-shrink: 0;
}
.header-img img {
  width: 100%;
  height: 100%;
  display: block;
}
.header-title {
  font-size: 18px;
  font-weight: 500;
  margin-left: 10px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
