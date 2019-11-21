<template>
  <div>
    <div v-if="loading" class="spinner-border" role="status">
      <span class="sr-only">Loading...</span>
    </div>
    <div v-else class="login-div col-6 offset-3">
      <div v-if="errors.length" class="error-list alert alert-danger">
        <div v-for="(error, idx) in errors" :key="idx">{{error}}</div>
      </div>
      <div class="form-group">
        <label for="id">ID</label>
        <input id="id" class="form-control" type="text" v-model="credential.username">
      </div>
      <div class="form-group">
        <label for="password">PASSWORD</label>
        <input id="password" class="form-control" type="password" v-model="credential.password">
      </div>
      <button class="btn btn-primary" @click="login">로그인</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import router from '../router'
export default {
  data(){
    return {
      credential: {
        username: '',
        password: ''
      },
      loading: false,
      errors: [],
    }
  },
  methods: {
    login(){
      if (this.checkForm()) {        
        console.log('로그인 시도 !!!!!!!!!!!!')
        axios.post('http://localhost:8000/api-token-auth/', this.credential)
        .then((res)=>{
          this.loading = true
          // this.$session.start()
          // this.$session.set('jwt', res.data.token)

          this.$store.dispatch('login', res.data.token)
  
          router.push('/')
        })
        .catch((e)=>{
          console.log(e)
          this.loading = true
        })
      }
    },
    checkForm(){
      this.errors = []
      if (this.credential.password.length < 8) {
        this.errors.push("비밀번호는 8글자가 넘어야합니다.")
      }
      if (!this.credential.username) {
        this.errors.push("아이디를 입력해주세요")
      }
      console.log(this.errors)
      if (this.errors.length === 0) {
        return true
      }
    }
  }
}
</script>

<style>

</style>