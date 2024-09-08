<template>
  <div class="chats">
    <button class="chat-btn" v-for="chat in chats" :key="chat.id" @click="emits('selectChat', chat.id)">
      <div class="chat-img">
        <img :src="chat.img" alt="avatar" />
      </div>
      <div class="chat-cont">
        <div class="chat-title-n-time">
          <div class="chat-title">{{ chat.title }}</div>
          <span class="chat-last-message-time">{{ chat.lastMessageTime }}</span>
        </div>
        <div class="chat-last-message">
          {{ chat.lastMessage }}
        </div>
      </div>
      <div class="chat-arrow">
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M10 7L15 12L10 17" stroke="#000000" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
        </svg>
      </div>
    </button>
  </div>
</template>

<script setup>
defineProps({
  chats: {
    type: Array,
    default: () => [],
  },
});

const emits = defineEmits("selectChat");
</script>

<style scoped>
.chats {
  width: 100%;
  padding: 24px 8px;
}
.chat-btn {
  width: 100%;
  background-color: #fff;
  border: 0;
  text-align: left;
  max-width: 100%;
  padding: 16px 0;
  padding-left: 72px;
  padding-right: 32px;
  overflow: hidden;
  cursor: pointer;
  margin-bottom: 8px;
  border-radius: 4px;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.01), 0 2px 2px rgba(0, 0, 0, 0.01), 0 4px 4px rgba(0, 0, 0, 0.01), 0 8px 8px rgba(0, 0, 0, 0.01), 0 16px 16px rgba(0, 0, 0, 0.01);
  position: relative;
}
.chat-img {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  overflow: hidden;
  flex-shrink: 0;
  float: left;
  margin-left: -64px;
}
.chat-img img {
  width: 100%;
  height: 100%;
  display: block;
}
.chat-cont {
  padding-left: 8px;
}
.chat-title-n-time {
  width: 100%;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
}
.chat-title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: calc(100% - 56px);
  font-size: 18px;
  padding-top: 4px;
}
.chat-last-message {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 100%;
  font-size: 12px;
  opacity: 0.5;
  margin-top: 2px;
}
.chat-last-message-time {
  font-size: 10px;
  margin-right: 2px;
  opacity: 0.5;
  position: absolute;
  top: 8px;
  right: 24px;
}
.chat-arrow {
  width: 16px;
  height: 100%;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  background-color: #fafafa;
  display: flex;
  align-items: center;
  justify-content: center;
}
.chat-arrow svg {
  width: 16px;
  height: auto;
  display: block;
  opacity: 0.3;
}
</style>
