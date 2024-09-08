<template>
  <div
    class="message-item"
    :class="{
      '--sent': message.sender === 'user',
      '--received': message.sender === 'admin',
    }"
  >
    <div class="author-img">
      <img src="https://placehold.jp/5090f7/ffffff/150x150.png" v-if="message.sender === 'user'" />
      <img src="https://placehold.jp/f750d3/ffffff/150x150.png" v-else />
    </div>
    <div class="message-bubble">
      <div class="message-content">{{ message.text }}</div>
      <div class="message-by">{{ authorDict[message.sender] }} в {{ message.time }}</div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  message: {
    type: Object,
    required: true,
  },
});

const authorDict = {
  user: "Вы",
  admin: "Менеджер",
};
</script>

<style scoped>
.message-item {
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  margin-bottom: 16px;
}

.message-item.--sent {
  flex-direction: row-reverse;
}
.message-item.--received {
}

.author-img {
  width: 56px;
  height: 56px;
  background: #ccc;
  border-radius: 50%;
  overflow: hidden;
}
.author-img img {
  width: 100%;
  height: auto;
  display: block;
}
.message-bubble {
  padding: 10px;
  margin: 0 10px 0;
  border-radius: 10px;
  color: #38472e;
  font-size: 18px;
  line-height: 1.3;
}
.message-item.--sent .message-bubble {
  background: #e2ffc7;
  width: fit-content;
  max-width: 70%;
}
.message-item.--received .message-bubble {
  background: #ffffff;
  width: fit-content;
  max-width: 70%;
}

.message-content {
}

.message-by {
  font-size: 10px;
  text-align: right;
  opacity: 0.5;
  margin-top: 8px;
}
</style>
