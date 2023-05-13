<script setup>
import { computed, ref } from "vue";
import ChatBubble from "@/components/ChatBubble.vue";

// Define props for conversations
const props = defineProps({
  conversations: {
    type: Array,
    required: true,
  },
});

// Initialize index of the selected conversation
const selectedConversationIndex = ref();

// Compute the current conversation based on the selected index
const currentConversation = computed(() => {
  return props.conversations[selectedConversationIndex.value];
});

// Define search and newMessage as ref's
const search = ref("");
const newMessage = ref("");

// Filtered conversations based on search input
const filteredConversations = computed(() => {
  return props.conversations.filter(conversation =>
    conversation.title.toLowerCase().includes(search.value.toLowerCase())
  );
});

// Emit function for sending a new message
const emit = defineEmits(['new-message']);
const sendMessage = () => {
  if (newMessage.value.trim() !== "") {
    // Emit a new-message event with the new message
    emit('new-message', newMessage.value.trim());
    newMessage.value = "";
  }
};

</script>


<template>
  <div class="flex gap-2 text-black w-full m-4">
    <div class="flex flex-col w-1/5 bg-indigo-100 rounded p-3">
      <!-- Add a search bar to filter conversations -->
      <input
        v-model="search"
        placeholder="Search conversations..."
        class="mb-2 p-2 rounded border-2 border-gray-200"
      />
      <div
        @click="selectedConversationIndex = index"
        v-for="(conversation, index) in filteredConversations"
        :key="index"
        class="p-2 rounded m-1 cursor-pointer hover:bg-indigo-200"
      >
        <span class="font-bold">{{ conversation.title }}</span>
      </div>
    </div>
    <div class="flex flex-col w-4/5 bg-indigo-200 rounded h-[90vh]">
      <div v-if="currentConversation != null" class="flex flex-col w-full px-2 h-full overflow-y-auto">
        <chat-bubble
          v-for="(message, index) in currentConversation.messages"
          :key="index"
          :message="message"
        ></chat-bubble>
        <!-- Add a text input for sending messages -->
        <input
          v-model="newMessage"
          @keyup.enter="sendMessage"
          placeholder="Type your message..."
          class="mt-2 p-2 rounded border-2 border-gray-200"
        />
      </div>
      <div v-else class="flex justify-center items-center h-full w-full">
        <span>Please select a conversation first.</span>
      </div>
    </div>
  </div>
</template>
