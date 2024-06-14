
<template>
  <input type="text" v-model="userName" placeholder="name">
  <input type="email" v-model="userEmail" name="email" placeholder="email">
  <input type="password" v-model="userPass" name="password" placeholder="password">
  <input type="button" @click="sendData()" value="Send">
  
    <div v-if="users.length == 0" className="user">User list is empty</div>
    <div v-else-if="users.length == 1" className="user">User has one element</div>
    <div v-else className="user">User has more than one element</div>

  <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser" />

  <p className="error">{{ error }}</p>


  <p>{{ users }}</p>
</template>

<script>

import User from './components/User.vue';

export default {
  components: { User },
  data() { 
    return {
      users: [],
      error: '',
      userName: '',
      userEmail: '',
      userPass: ''
    }
  }, 
  methods: {
    sendData(val) { 
      if (this.userName == '') {
        this.error = 'empty name';
        return;
      }
      else if (this.userEmail == '') {
        this.error = 'empty email';
        return;
      }
      else if (this.userPass == '') {
        this.error = 'empty pass';
        return;
      }

      this.error = '';

      this.users.push({
        name: this.userName,
        email: this.userEmail,
        pass: this.userPass,
      })
    },
    deleteUser(index) {
      this.users.splice(index, 1);
    }
  }
}
</script>

<style scoped>

  input {
    display: block;
    margin-bottom: 10px;
    border-radius: 3px;
    border: 1px solid silver;
    outline: none;
    padding: 10px 15px;
    background: #fafafa;
    color: #333;
  }

  button {
    border: 0;
    border-radius: 5px;
    outline: none;
    padding: 10px 15px;
    background-color: #6cd760;
    color: #167f3d;
    font-weight: bold;
    cursor: pointer;
    transition: transform 500ms ease;
  }

  button:hover {
    transform: translateY(-5px);
  }

  .user {
    width: 500px;
    margin-top: 20px;
    border: 1px solid silver;
    background: #e3e3e3;
    color: #222;
    padding: 20px;
    border-radius: 5px;
  }
</style>
