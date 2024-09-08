<template>
  <div class="wrapper">
    <div class="content-inner">
      <ChatItem v-if="selectedChatId" :key="selectedChatId" :currentChat="chats.find((el) => el.id === selectedChatId)" @selectChat="selectChat" />
      <ChatsList :chats="chats" @selectChat="selectChat" v-else />
    </div>
  </div>
</template>

<script setup>
import ChatItem from "./components/ChatItem.vue";
import ChatsList from "./components/ChatsList.vue";

import { ref } from "vue";

const selectedChatId = ref(null);

const selectChat = (id) => {
  selectedChatId.value = id;
};

const chats = ref([
  {
    id: 1,
    img: "https://placehold.jp/5090f7/ffffff/150x150.png",
    title: "Пример названия",
    lastMessageTime: "12:00:31",
    lastMessage: "Последнее сообщение в этом чате может быть длинным и уходит в многоточие",
  },
  {
    id: 2,
    img: "https://placehold.jp/f75082/ffffff/150x150.png",
    title: "Другое название в этот раз длинное чтобы убедиться как оно выглядит",
    lastMessageTime: "12:00:51",
    lastMessage: "Последнее сообщение в этом чате может быть длинным и уходит в многоточие",
  },
  {
    id: 3,
    img: "https://placehold.jp/61ad35/ffffff/150x150.png",
    title: "Еще одно название",
    lastMessageTime: "12:00:11",
    lastMessage: "Последнее сообщение в этом чате может быть длинным и уходит в многоточие",
  },
  {
    id: 4,
    img: "https://placehold.jp/f750d3/ffffff/150x150.png",
    title: "Еще одно название",
    lastMessageTime: "12:00:21",
    lastMessage: "Последнее сообщение в этом чате может быть длинным и уходит в многоточие",
  },
]);
</script>

<style scoped>
.wrapper {
  display: flex;
  height: 100%;
  width: 100%;
}
.content-inner {
  max-width: 600px;
  width: 100%;
  margin: 0 auto;
  height: 100%;
}
</style>
