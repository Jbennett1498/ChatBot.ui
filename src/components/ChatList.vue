<script setup>
  import { defineProps } from 'vue';

  const props = defineProps({
    chats: Array,
    selectedChat: Object
  });
</script>

<template>
  <div class="chat-list">
    <div 
      v-for="chat in chats" 
      :key="chat.id" 
      :class="['chat-item', { active: chat.id === selectedChat?.id }]"
      @click="$emit('select', chat)"
    >
      {{ chat.name }}
    </div>
  </div>
</template>

<style scoped>
.chat-list {
  display: flex;
  flex-direction: column;
  font-weight: bold;
  background-color: #fff;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.chat-item {
  padding: 12px 16px;
  cursor: pointer;
  background: #f5f5f5;
  border-bottom: 1px solid #E0e8e6;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

.chat-item:hover {
  background-color: #a9d6e5; 
  transform: translateX(5px); /* Slightly shifts the item when hovered */
}

.chat-item.active {
  background-color: #c0d6df;
  color: #081c15;
}

.chat-item:last-child {
  border-bottom: none;
}
</style>


