<template>
  <div class="input-area">
    <form class="form" @submit.prevent="sendMessage">
      <div class="text-area-wrapper">
        <textarea class="text-area" placeholder="Введите ваше сообщение..." @input="textareaChange" @keydown="handleKeyDown" ref="textareaRef" v-model="message"></textarea>
      </div>
      <button class="send">
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M11.5003 12H5.41872M5.24634 12.7972L4.24158 15.7986C3.69128 17.4424 3.41613 18.2643 3.61359 18.7704C3.78506 19.21 4.15335 19.5432 4.6078 19.6701C5.13111 19.8161 5.92151 19.4604 7.50231 18.7491L17.6367 14.1886C19.1797 13.4942 19.9512 13.1471 20.1896 12.6648C20.3968 12.2458 20.3968 11.7541 20.1896 11.3351C19.9512 10.8529 19.1797 10.5057 17.6367 9.81135L7.48483 5.24303C5.90879 4.53382 5.12078 4.17921 4.59799 4.32468C4.14397 4.45101 3.77572 4.78336 3.60365 5.22209C3.40551 5.72728 3.67772 6.54741 4.22215 8.18767L5.24829 11.2793C5.34179 11.561 5.38855 11.7019 5.407 11.8459C5.42338 11.9738 5.42321 12.1032 5.40651 12.231C5.38768 12.375 5.34057 12.5157 5.24634 12.7972Z" stroke="#000000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
        </svg>
      </button>
    </form>
    <label class="file-attach" for="file-input">
      <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M20 10.9696L11.9628 18.5497C10.9782 19.4783 9.64274 20 8.25028 20C6.85782 20 5.52239 19.4783 4.53777 18.5497C3.55315 17.6211 3 16.3616 3 15.0483C3 13.7351 3.55315 12.4756 4.53777 11.547L12.575 3.96687C13.2314 3.34779 14.1217 3 15.05 3C15.9783 3 16.8686 3.34779 17.525 3.96687C18.1814 4.58595 18.5502 5.4256 18.5502 6.30111C18.5502 7.17662 18.1814 8.01628 17.525 8.63535L9.47904 16.2154C9.15083 16.525 8.70569 16.6989 8.24154 16.6989C7.77738 16.6989 7.33224 16.525 7.00403 16.2154C6.67583 15.9059 6.49144 15.4861 6.49144 15.0483C6.49144 14.6106 6.67583 14.1907 7.00403 13.8812L14.429 6.88674" stroke="#000000" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      </svg>
    </label>
    <input type="file" class="file-input" id="file-input" ref="fileInputRef" @change="handleFileChange" />
  </div>
</template>

<script setup>
import { ref } from "vue";

const emits = defineEmits(["sendMessage"]);

const fileInputRef = ref(null);
const handleFileChange = (e) => {
  const file = e.target.files[0];
  if (file) {
    alert("Тут загрузка файла");
  }
};

const message = ref("");

const sendMessage = () => {
  emits("sendMessage", message.value);
  message.value = "";
};

const textareaRef = ref(null);

const textareaChange = (e) => {
  const el = e.target;

  if (message.value.trim() === "") {
    el.style.height = "24px";
    return;
  }

  el.style.height = "auto";
  el.style.height = el.scrollHeight + "px";
};

const handleKeyDown = (e) => {
  if (e.key === "Enter") {
    sendMessage();
  }
};
</script>

<style scoped>
.input-area {
  width: 100%;
  display: flex;
  color: #ccc;
  padding: 8px;
  flex-shrink: 0;
  background-color: #ededed;
}

.form {
  width: 100%;
  background: #fff;
  height: 100%;
  border-radius: 30px;
  display: flex;
  justify-content: space-around;
}
.text-area-wrapper {
  padding: 8px;
  padding-left: 16px;
  width: 100%;
}
.text-area {
  display: block;
  width: 100%;
  background: transparent;
  height: 24px;
  max-height: 140px;
  border: 0;
  padding: 0;
  padding-top: 2px;
  resize: none;
  font-size: 18px;
  line-height: 1.2;
  color: #1e2427;
  outline: none;
  overflow-y: auto;
  scrollbar-width: thin;
  scrollbar-color: #888 #f1f1f1;
}
.text-area::placeholder {
  color: #5b6870;
}

.send {
  flex-shrink: 0;
  background: #fff;
  width: 40px;
  height: 40px;
  padding: 10px;
  color: #fff;
  border: none;
  margin: 0 10px;
  border-radius: 50%;
  cursor: pointer;
}
.send svg * {
  stroke: #38472e;
}

.file-attach {
  flex-shrink: 0;
  background: #fff;
  width: 40px;
  height: 40px;
  padding: 8px;
  color: #fff;
  border: none;
  margin-left: 16px;
  border-radius: 50%;
  cursor: pointer;
}
.file-attach svg * {
  stroke: #38472e;
}
.file-input {
  position: absolute;
  left: -9999px;
  opacity: 0;
}
</style>
