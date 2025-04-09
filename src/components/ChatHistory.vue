<template>
  <!-- Chat Header -->
  <div v-if="!isExpanded" class="chat-header">
      <button class="backbtn" @click="$emit('back')">←</button>
      <h4>{{ chat.name }}</h4>
  </div>

  <!-- Chat Messages -->
  <div class="chat-history">
    <div v-for="(msg, idx) in chat.history" :key="idx" :class="['msg', msg.sender]">
      <div v-if="msg.sender === 'user' || msg.sender === 'human'" class="user-message">
        <p>{{ msg.content }}</p>
      </div>
      <div v-else class="bot-message">
        <p><strong>ChatBot:</strong></p>
        <p v-html="parseMarkdown(msg.content)"></p>
      </div>
    </div>

    <div class="input-container">
      <input
        type="text"
        placeholder="Type your message..."
        class="message-input"
      />

      <button class="icon-btn">
        <img src="../assets/send.svg" alt="Send" />
      </button>

       <!-- Btn to view the source's from this view (not implemented)-->
      <button v-if="!isExpanded" class="icon-btn">
        <img src="../assets/source.svg" alt="Source" />
      </button>
    </div>
  </div>
  
</template>

<script setup>
  import { ref, defineEmits} from 'vue';
  import { marked } from 'marked';  
  import ChatSourcePanel from './ChatSourcePanel.vue';

  // Prop for the chat data
  const props = defineProps({
    chat: Object,
    isExpanded: Boolean
  });

  const emit = defineEmits(['back']); 
  
  // Function to parse the markdown content to HTML
  const parseMarkdown = (content) => {
    return marked(content);
  };
</script>

<style scoped>
.chat-header {
  position: sticky;
  background: #f4f4f5;
  color: #081c15;
  padding: 10px;
  display: flex;
  align-items: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); 
}

.chat-header h4 {
  margin: 0;
}

.backbtn {
  background: none;
  border: none;
  padding: 5px 10px;
  font-size: 18px;
  cursor: pointer;
}
.chat-history {
  flex: 1;
  overflow-y: auto;
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  position: relative;
}

.msg {
  margin-bottom: 10px;
  text-align: left;
}

.msg.user, .msg.human {
  text-align: left;
  padding: 10px;
  max-width: 65%;
  margin-left: auto;
  margin-right: 10px;
  background-color: #a9d6e5; 
  color: #081c15;
  border-radius: 15px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.msg.user p, .msg.human p {
  margin: 5px 0;
}

.msg.bot {
  padding: 10px;
  max-width: 60%;
  margin-right: auto;
  margin-left: 10px;
  background-color: #f1f1f1; 
  color: #081c15;
  border-radius: 15px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.msg.bot p, .msg.user p {
  margin: 5px 0;
}

.input-container {
  position: sticky;
  bottom: 0;
  background: white;
  padding: 10px;
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 10px;
}

.message-input {
  width: 80%;
  padding: 10px;
  border-radius: 10px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

.icon-btn {
  background: none;
  border: none;
  padding: 10px;
  cursor: pointer;
}

.icon-btn img {
  width: 20px;
  height: 20px;
}

</style>
