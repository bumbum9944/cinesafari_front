<template>
  <div class="signup-form-page">
    <div class="login-div col-6 offset-3">
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
      <div class="form-group">
        <label for="password-confirm">PASSWORD 확인</label>
        <input id="password-confirm" name="password_confirmation" class="form-control" type="password" v-model="credential.passwordConfirm">
      </div>
      <button class="btn btn-primary" @click="signUp">회원가입</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import router from '../router'
export default {
  name: "loginform",
  data(){
    return {
      credential: {
        username: '',
        password: '',
        passwordConfirm: ''
      },
      errors: [],
    }
  },
  methods: {
    signUp(){
      if (this.checkForm()) {        
        axios.post('http://localhost:8000/api-auth/signup/', {username: this.credential.username, password: this.credential.password})
        .then((res)=>{
          console.log(res)
          router.push('/')
        })
        .catch((e)=>{
          console.log(e)
        })
      }
    },
    checkForm(){
      this.errors = []
      if (this.credential.password.length < 8) {
        this.errors.push("비밀번호는 8글자가 넘어야합니다.")
      }
      if (this.credential.password !== this.credential.passwordConfirm) {
        this.errors.push("비밀번호가 같지 않습니다.")
      }
      if (!this.credential.username) {
        this.errors.push("아이디를 입력해주세요")
      }
      // console.log(this.errors)
      if (this.errors.length === 0) {
        return true
      }
    }
  }
}
</script>

<style>

</style>