<script setup>
import ChatList from "@/components/ChatList.vue";
import { ref } from "vue";

const conversations = ref([]);

const addConversation = (title, messages = [], username) => {
  conversations.value.push({ title, messages, username });
};


const startNewConversation = () => {
  fetch('https://randomuser.me/api/?format=json')
    .then(response => response.json())
    .then(data => {
      // Extract the user's name from the response
      const user = data.results[0];
      const username = user.login.username;
      
      // Add the new conversation with the random user's name as the title
      addConversation(`Chat with ${username}`, [], username);
    })
    .catch(error => {
      console.error('Error fetching user:', error);
    });
};

fetch('https://randomuser.me/api/')
  .then(response => response.json())
  .then(data => {
    // Extract the user information from the response
    const user = data.results[0];
    
    // Access the user's name and other details
    const firstName = user.name.first;
    const lastName = user.name.last;
    const username = user.login.username;
    
    // You can use the extracted user details here if needed
  })
  .catch(error => {
    console.error('Error fetching user:', error);
  });
const addMessageToConversation = (conversationIndex, message) => {
  const conversation = conversations.value[conversationIndex];

  if (conversation) {
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

startNewConversation("Omer");

addMessageToConversation(2, {
  outgoing: true,
  text: "Hi Omer!",
  username: "e7pm",
});

// ... and so on for other conversations
</script>

<template>
  <div class="container flex justify-center">
    <ChatList
      :conversations="conversations"
      :handleNewMessage="handleNewMessage"
    ></ChatList>
  </div>
</template>
