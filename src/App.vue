<template>
  <div class="wrapper">
    <div class="inner">
      <MessagesList :messages="messages" ref="messagesListRef" />
      <MessageInput @send-message="handleSend" />
    </div>
  </div>
</template>

<script setup>
import { nextTick, onMounted, ref } from "vue";
import MessageInput from "./components/MessageInput.vue";
import MessagesList from "./components/MessagesList.vue";

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
.wrapper {
  background: #ede6de;
  padding: 8px;
  height: 100%;
}
.inner {
  max-width: 600px;
  margin: 0 auto;
  height: 100%;
  display: flex;
  flex-direction: column;
}
</style>
