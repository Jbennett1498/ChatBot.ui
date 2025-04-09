<script setup>
  import { defineProps, defineEmits } from 'vue';
  import ChatHistory from './ChatHistory.vue';
  import ChatList from './ChatList.vue';
  import closeIcon from '../assets/cross-circle.svg';
  import expandIcon from '../assets/expand.svg';

  const props = defineProps({
    chats: Array,
    selectedChat: Object,
    isExpanded: Boolean
  });

  const emit = defineEmits(['close', 'expand', 'select-chat']);

  const close = () => emit('close');
  const expand = () => emit('expand');
  const selectChat = (chat) => emit('select-chat', chat);
  const goBack = () => emit('select-chat', null); 
</script>

<template>
  <div class="chat-window">
    <div class="chat-header">
      <button @click="close" class="header-button">
        <img :src="closeIcon" alt="Close" />
      </button>

      <h3>ChatBot.io</h3>
      
      <button @click="expand" class="header-button">
        <img :src="expandIcon" alt="Expand" />
      </button> 
    </div>

    <ChatHistory 
      v-if="selectedChat" 
      :chat="selectedChat" 
      :is-expanded="isExpanded" 
      @back="goBack" 
    />

    <ChatList
      v-else
      :chats="chats"
      :selected-chat="selectedChat"
      @select="selectChat"
    />
  </div>
</template>

<style scoped>
.chat-window {
  position: fixed;
  bottom: 20px;
  right: 20px;
  display: flex;
  flex-direction: column;
  height: 85%;
  width: 500px;
  background: white;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  overflow: hidden;
  z-index: 1000;
}

.chat-header {
  display: flex;
  justify-content: space-between;
  background: #6096ba;
  color: #081c15;
  padding: 10px;
}

.header-button{
  background: transparent;
  border: none;
  cursor: pointer;
}
</style>
