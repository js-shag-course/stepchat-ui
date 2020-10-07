<template>
  <div id="app">
    <Messages :messages="messagesList" />
    <Users :users="usersList" />
    <MessageForm />
    <RegisterForm />
  </div>
</template>

<script>
import Messages from '@/components/Messages'
import Users from '@/components/Users'
import MessageForm from '@/components/MessageForm'
import RegisterForm from '@/components/RegisterForm'

export default {
  name: 'App',
  components: {
    Messages,
    Users,
    MessageForm,
    RegisterForm
  },
  data: function () {
    return {
      root: 'http://localhost:3000', // TODO: api.stepchat.site
      user: 'http://localhost:3000/user',
      message: 'http://localhost:3000/message',
      messagesList: null,
      usersList: null
    }
  },
  async beforeMount () {
    setInterval(async () => {
      const response = await fetch(this.root)
      if (response.ok) {
        const data = await response.json()
        this.messagesList = data.messages
        this.usersList = data.users
      }
    }, 1000)
  }
}
</script>

<style lang="scss">
</style>
