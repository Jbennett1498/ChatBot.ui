<template>
  <div id="app">
    <ChatIcon v-if="!isChatOpen" @open="isChatOpen = true" />
    
    <ChatWindow 
      v-if="isChatOpen && !isExpanded" 
      :chats="chats"
      :selected-chat="selectedChat"
      :is-expanded="isExpanded"
      @close="isChatOpen = false" 
      @expand="isExpanded = true"
      @select-chat="selectChat"
    />

    <ExpandedChat 
      v-if="isExpanded" 
      :chats="chats"
      :selected-chat="selectedChat"
      @close="() => { isExpanded = false; isChatOpen = false; }"
      @collapse="isExpanded = false"
      @select-chat="selectChat"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import ChatIcon from './components/ChatIcon.vue';
import ChatWindow from './components/ChatWindow.vue';
import ExpandedChat from './components/ExpandedChat.vue';
import chatsData from './data/chats.json';

const isChatOpen = ref(false);
const isExpanded = ref(false);
const selectedChat = ref(null);
const chats = ref(chatsData);

function selectChat(chat) {
  selectedChat.value = chat;
}
</script>


