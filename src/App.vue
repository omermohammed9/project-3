<script setup>
import ChatList from "@/components/ChatList.vue";
import {ref} from "vue";

const conversations = ref([]);

const addConversation = (title, messages = [], username) => {
  conversations.value.push({ title, messages, username });
};


const startNewConversation = (username) => {
  addConversation(`Chat with ${username}`, [], username);
};


const addMessageToConversation = (conversationIndex, message) => {
  const conversation = conversations.value[conversationIndex];
  
  if(conversation) {
    conversation.messages.push(message);
  } else {
    console.error(`No conversation found at index ${conversationIndex}`);
  }
};

// Add the new function here
const handleNewMessage = (conversationIndex, text) => {
  const conversation = conversations.value[conversationIndex];
  if (conversation) {
    addMessageToConversation(conversationIndex, {
      outgoing: true,
      text: text,
      username: conversation.username, // Use the username from the conversation
    });
  } else {
    console.error(`No conversation found at index ${conversationIndex}`);
  }
};


// Add initial conversations
startNewConversation("Abdulazeez");
addMessageToConversation(0, {
  outgoing: true,
  text: "Hello, World!",
  username: "hdrm147",
});

addMessageToConversation(0, {
  outgoing: false,
  text: "Hello, Abdulazeez!",
  username: "azeez",
});

startNewConversation("Ahmed");
addMessageToConversation(1, {
  outgoing: true,
  text: "Hi Ahmed!",
  username: "hdrm147",
});

// ... and so on for other conversations
</script>

<template>
  <div class="container flex justify-center">
    <ChatList :conversations="conversations" :handleNewMessage="handleNewMessage"></ChatList>
  </div>
</template>
