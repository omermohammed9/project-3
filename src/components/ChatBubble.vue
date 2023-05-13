<script setup>
// Define props for the message
const props = defineProps({
  message: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div
    v-if="message"
    class="p-2 m-1 rounded border-2 border-gray-200"
    :class="{
      'bg-green-100': message.outgoing,
      'bg-blue-100': !message.outgoing,
    }"
  >
    <p>
      <strong>{{ message.username }}</strong>
    </p>
    <p>{{ message.text }}</p>
  </div>
</template>
