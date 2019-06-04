<template>
  <div>
    <!-- 登录 -->
    <form v-if="!isReg">
      <div>username: </div>
      <input type="text" v-model="username">
      <div>password: </div>
      <input type="password" v-model="password">
      <button type="button" @click="login()">login</button>
      <button type="button" @click="register()">sign up</button>
    </form>
    <!-- 注册 -->
    <form v-else>
      <div>username:</div>  
      <input type="text" v-model="username">
      <div>password: </div>
      <input type="password" v-model="password">
      <div>repeat password: </div>
      <input type="password" v-model="repeat">
      <button type="button" @click="addUser()">sign up</button>
      <button type="button" @click="cancel()">cancel</button>
    </form>
  </div>
</template>
<script>
export default {
  name: "login",
  data() {
    return {
      isReg: false,
      username: '',
      password: '',
      repeat: ''
    }
  },
  methods: {
    addUser() {
      if(this.password === this.repeat) {
        localStorage.setItem('username', this.username) 
        localStorage.setItem('password', this.password)
        this.username = ''
        this.password = ''
        this.isReg = false
      }else {
        alert('两次秘密不匹配')
      }
    },
    cancel() {
      this.isReg = false
    },
    login() {
      if(localStorage.getItem('username') === this.username && localStorage.getItem('password') === this.password) {
        this.$router.push('/home/list')
        this.username = ''
        this.password = ''
      }else {
        alert('登录名或密码错误')
      }
    },
    register() {
      this.isReg = true
    }
  }
}
</script>