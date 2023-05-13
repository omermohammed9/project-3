
<script setup>
import ChatList from "@/components/ChatList.vue";
import {ref} from "vue";
const conversations = ref([]);
const addConversation = (title, messages) => {
  conversations.value.push({ title, messages });
};

addConversation("Chat with Abdulazeez", [
  {
    outgoing: true,
    text: "Hello, World!",
    username: "hdrm147"
  },
  {
    outgoing: false,
    text: "Hello, Haidar!",
    username: "azeez"
  }
]);

addConversation("Chat with Ahmed", [
  {
    outgoing: true,
    text: "Loooop",
    username: "hdrm147"
  },
  {
    outgoing: false,
    text: "Hello, Haidar!",
    username: "azeez"
  }
]);

addConversation("Chat with Ahmed", [
  {
    outgoing: true,
    text: "Loooop",
    username: "hdrm147"
  },
  {
    outgoing: false,
    text: "Hello, Haidar!",
    username: "azeez"
  }
]);
addConversation("Chat with Ali", [
  {
    outgoing: true,
    text: "Loooop",
    username: "hdrm147"
  },
  {
    outgoing: false,
    text: "Hello, Haidar!",
    username: "azeez"
  }
]);
addConversation("Chat with Mohammed", [
  {
    outgoing: true,
    text: "Loooop",
    username: "hdrm147"
  },
  {
    outgoing: false,
    text: "Hello, Haidar!",
    username: "azeez"
  }
]);



</script>


<template>
  <div 
        class="container flex justify-center">
        <ChatList :conversations="conversations"></ChatList>
        </div>
</template>
