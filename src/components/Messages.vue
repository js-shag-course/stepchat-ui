<template>
  <div v-chat-scroll>
    <div
      v-for="(message, i) in messages"
      :key="i"
      :class="messageClasses(message.name)"
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
    messages: Array,
    userName: String
  },
  methods: {
    messageClasses (name) {
      return this.userName === name
        ? ['one-message', 'out-message']
        : ['one-message']
    }
  }

}
</script>

<style lang="scss">
  .one-message {
    box-sizing: border-box;
    border: 2px solid #53A2BD;
    padding: 5px 10px;
    margin: 5px 0;
    border-radius: 10px;
    span {
      display: block;
      opacity: .75;
      font-size: 10px;
    }

    &.out-message {
      align-self: flex-end;
    }
  }
</style>
