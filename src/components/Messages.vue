<template>
  <div>
    <div
      class="message"
      v-for="(message, i) in messages"
      :key="i"
    >
      <span>{{ message.name }}:</span>
      <div>{{ message.text }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Messages',
  props: {
    messages: Array
  }
}
</script>
