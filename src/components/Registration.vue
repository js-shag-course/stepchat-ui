<template>
<div>
  <div class="reg-form">
    <h3>Регистрация</h3>
    <label>
      <span>Логин</span>
      <input v-model="login" type="text" />
    </label>
    <label>
      <span>Пароль</span>
      <input v-model="password" type="password" />
    </label>
    <label>
      <span>Имя</span>
      <input v-model="name" type="text" />
    </label>
    <label>
      <span>Аватарка</span>
      <br> В процессе. :)
    </label>
    <button @click="$emit('send-query', message)">Зарегистрироваться</button>
  </div>
</div>
</template>

<script>
export default {
  name: 'Registration',
  data: () => ({
    login: null,
    password: null,
    name: null
  }),
  computed: {
    message () {
      return {
        action: 'register',
        payload: {
          login: this.login,
          password: this.password,
          name: this.name
        }
      }
    }
  }
}
</script>

<style lang="scss">
 .reg-form {
   label, span {
     display: block;
   }
 }
</style>
