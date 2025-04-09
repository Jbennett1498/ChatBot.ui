<script setup>
  import { defineProps, defineEmits } from 'vue';
  import ChatList from './ChatList.vue';
  import ChatHistory from './ChatHistory.vue';
  import ChatSourcePanel from './ChatSourcePanel.vue'
  import closeIcon from '../assets/cross-circle.svg';
  import collapseIcon from '../assets/collapse.svg';

  const props = defineProps({
    chats: Array,
    selectedChat: Object
  });

  const emit = defineEmits(['close', 'collapse', 'select-chat']);

  const close = () => emit('close');
  const collapse = () => emit('collapse');
  const selectChat = (chat) => emit('select-chat', chat);
</script>

<template>
  <!-- Header -->
  <div class="expanded-chat">
    <div class="header">
      <button @click="close" class="header-button">
        <img :src="closeIcon" alt="close" />
      </button>

      <h3>ChatBot.io</h3>

      <button @click="collapse" class="header-button">
        <img :src="collapseIcon" alt="collapse" />
      </button>
    </div>

    <!-- sections -->
    <div class="layout">
      <ChatList
        :chats="chats"
        :selected-chat="selectedChat"  
        @select="selectChat"
      />

      <ChatHistory
        v-if="selectedChat"
        :chat="selectedChat"
        :is-expanded="true"
      />

      <ChatSourcePanel
        v-if="selectedChat"
        :chat="selectedChat"
        :is-expanded="true"
      />
      
      <div v-else class="placeholder">Select a chat to view conversation</div>
    </div>
  </div>
</template>

<style scoped>
.expanded-chat {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: white;
  display: flex;
  flex-direction: column;
  z-index: 9999;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  background: #6096ba;
  color: #081c15;
  font-weight: bold;
}

.header-button{
  background: transparent;
  border: none;
  cursor: pointer;
}

.layout {
  display: flex;
  flex: 1;
  overflow: hidden;
}

.layout > *:nth-child(1) {
  flex: 1; 
  overflow-y: auto;
  padding: 16px;
}

.layout > *:nth-child(2) {
  flex: 4; 
  overflow-y: auto;
  padding: 16px;
}

.layout > *:nth-child(3) {
  flex: 2; 
  overflow-y: auto;
  padding: 16px;
}


.placeholder {
  flex: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  font-style: italic;
  color: #888;
}
</style>
