<!-- ChatIcon.vue -->
<template>
  <button class="chat-icon" @click="$emit('open')"> 
    <img src="../assets/chat.svg" alt="Source" />
  </button>
</template>

<style scoped>
.chat-icon {
  position: fixed;
  bottom: 50px;
  right: 50px;
  font-size: 24px;
  background: #a9d6e5;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 50%;
  cursor: pointer;
}
</style>