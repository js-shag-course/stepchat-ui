<template>
  <div class="app">
    <header>
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 60 60">
        <path fill="#53A2BD" d="M10 25.465h13a1 1 0 100-2H10a1 1 0 100 2zM36 29.465H10a1 1 0 100 2h26a1 1 0 100-2zM36 35.465H10a1 1 0 100 2h26a1 1 0 100-2z"/>
        <path fill="#53A2BD" d="M54.072 2.535l-34.142-.07c-3.27 0-5.93 2.66-5.93 5.93v5.124l-8.07.017c-3.27 0-5.93 2.66-5.93 5.93v21.141c0 3.27 2.66 5.929 5.93 5.929H12v10a1 1 0 001.74.673l9.704-10.675 16.626-.068c3.27 0 5.93-2.66 5.93-5.929v-.113l5.26 5.786a1.002 1.002 0 001.74-.673v-10h1.07c3.27 0 5.93-2.66 5.93-5.929V8.465a5.937 5.937 0 00-5.928-5.93zM44 40.536a3.934 3.934 0 01-3.934 3.929l-17.07.07a1 1 0 00-.736.327L14 53.949v-8.414a1 1 0 00-1-1H5.93A3.934 3.934 0 012 40.606V19.465a3.935 3.935 0 013.932-3.93L15 15.516h.002l25.068-.052a3.934 3.934 0 013.93 3.93v21.142zm14-10.93a3.934 3.934 0 01-3.93 3.929H52a1 1 0 00-1 1v8.414l-5-5.5V19.395c0-3.27-2.66-5.93-5.932-5.93L16 13.514v-5.12a3.934 3.934 0 013.928-3.93l34.141.07h.002a3.934 3.934 0 013.93 3.93v21.142z"/>
      </svg>
      <h1>StepChat <span>v0.1</span></h1>
    </header>
    <Users :users="users" class="users-list" />
    <Messages
      :messages="messagesList"
      :user-name="userName"
      class="messages-list"
    />
    <MessageForm v-if="userName" class="form" @send-message="sendMessage" />
    <RegisterForm v-else class="form" @enter-chat="enterChat" />
    <footer>
      &copy; Stepchat 2020
    </footer>
  </div>
</template>

<script>
import randomstring from 'randomstring'

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
  data: () => ({
    root: 'http://api.stepchat.site', // TODO: api.stepchat.site
    user: 'http://api.stepchat.site/user',
    message: 'http://api.stepchat.site/message',
    messagesList: null,
    usersList: [],
    avatarsList: [],
    userName: null
  }),
  computed: {
    totalUsers () {
      return this.usersList.length
    },
    users () {
      const users = []
      for (let i = 0; i < this.totalUsers; i++) {
        users.push({
          name: this.usersList[i],
          avatar: this.avatarsList[i]
        })
      }

      return users
    }
  },
  watch: {
    totalUsers (newVal, oldVal) {
      if (oldVal === 0) {
        for (let i = 0; i < newVal; i++) {
          this.avatarsList.push('https://robohash.org/' + randomstring.generate(7))
        }
      }
      // TODO: Доделать!
      if (newVal > oldVal) {
        // +++
      } else {
        // ---
      }
    }
  },
  methods: {
    async enterChat (name) {
      const user = await fetch(this.user, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json;charset=utf-8' },
        body: JSON.stringify({ name: name })
      })
      if (user.ok) this.userName = name
    },
    async sendMessage (messageText) {
      const message = await fetch(this.message, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json;charset=utf-8' },
        body: JSON.stringify({ name: this.userName, text: messageText })
      })
      if (!message.ok) alert('Не удалось отправить сообщение, сорян... ')
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
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;700&display=swap');

  html, body {
    width: 100%;
    height: 100%;
    min-height: 100vh;
    margin: 0;
    padding: 0;
  }
  body {
    background: url('/images/bg.jpg') 50% 50% no-repeat;
    background-size: cover;
    font-family: 'Roboto', sans-serif;
    font-size: 14px;
    color: #2B2C28;
  }
  .app {
    display: grid;
    width: 90%;
    height: 100%;
    margin: 0 5%;
    grid-template-columns: 350px auto;
    grid-template-rows: 100px auto 70px 50px;
    grid-gap: 20px;
    grid-template-areas:
      "header header"
      "users messages"
      "options form"
      "footer footer";

    & > * {
      background: #fff;
      box-sizing: border-box;
      padding: 10px;
      border-radius: 10px;
      box-shadow: 0 0 10px 0 rgba(0,0,0,0.5);
    }
  }

  header {
    border-top-left-radius: 0 !important;
    border-top-right-radius: 0 !important;
    grid-area: header;

    display: flex;
    flex-direction: row;
    align-items: center;

    svg {
      display: block;
      width: 80px;
      height: auto;
      margin: 0 32px 0 0;
    }

    h1 {
      margin: 0;
      font-weight: 300;
      font-size: 48px;

      span {
        font-size: 32px;
        font-weight: 100;
      }
    }
  }

  .users-list {
    grid-area: users;
    overflow-y: scroll;
  }

  .messages-list {
    grid-area: messages;
    overflow-y: scroll;

    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }

  .form {
    grid-area: form;
  }

  footer {
    border-bottom-left-radius: 0 !important;
    border-bottom-right-radius: 0 !important;
    grid-area: footer;

    display: flex;
    align-items: center;

    font-weight: 300;
  }

</style>
