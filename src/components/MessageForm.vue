<template>
  <div>
    <div class="message-form">
      <input
        type="text"
        placeholder="Текст сообщения"
        v-model="message"
      />
      <button :disabled="message.length === 0" @click="sendMessage()">Отправить</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MessageForm',
  data: () => ({
    message: ''
  }),
  methods: {
    sendMessage () {
      this.$emit('send-message', this.message)
      this.message = ''
    }
  }
}
</script>

<style lang="scss">
  .message-form {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;

    input {
      flex-grow: 2;
      box-sizing: border-box;
      border-radius: 5px;
      padding: 0 10px;
      border: 1px solid #53A2BD;
      font-size: 16px;
      color: #2B2C28;
    }
    button {
      margin-left: 20px;
      box-sizing: border-box;
      border-radius: 5px;
      padding: 0 10px;
      border: 1px solid #53A2BD;
      font-size: 16px;
      cursor: pointer;
      background: #fff;
      color: #2B2C28;

      transition: all 300ms ease-in-out;

      &:hover {
        background: #53A2BD;
        color: #fff;
      }

      &:disabled {
        opacity: .5;
        cursor: not-allowed;
      }
      &:disabled:hover {
        background: #fff;
        color: #2B2C28;
      }
    }
  }
</style>
