<template>
  <div>
    <div class="one-user" v-for="(user, i) in users" :key="i" >
      <div class="avatar">
        <img :src="user.avatar" />
      </div>
      <div class="name">{{ user.name }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Users',
  props: {
    users: Array
  }
}
</script>

<style lang="scss">
 .one-user {
   display: flex;
   flex-direction: row;
   flex-wrap: nowrap;
   align-items: center;
   margin-bottom: 2px;
   .avatar {
     box-sizing: border-box;
     border: 2px solid #53A2BD;
     border-radius: 50%;
     overflow: hidden;
     margin-right: 2px;
     img {
       display: block;
       margin: 0;
       width: 32px;
       height: 32px;
     }
   }
   .name {
     overflow: hidden;
     white-space: nowrap;
   }
 }
</style>
