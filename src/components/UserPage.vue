<template>
  <div class="userPageView mx-3">
    <h1 class="">{{userNm}}'s Page</h1>
    <MyReviewList :myReviewList="myReviewList"/>
    <!-- <img src="https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile5.uf.tistory.com%2Fimage%2F25306D475647024305991C" style="height: 100%;" alt=""> -->
  </div>
</template>

<script>
import MyReviewList from "./MyReviewList"
import axios from "axios"
import jwtDecode from "jwt-decode"
export default {
  name: 'MserPageView',
  data(){
    return {
      myReviewList: [],
      userNm: ""
    }
  },
  props: {
  },
  components: {
    MyReviewList
  },
  methods: {
    myReviews(){
      this.$session.start()
      const token = this.$session.get('jwt')
      const decodedToken = jwtDecode(token)
      const user_id = decodedToken.user_id
      this.userNm = decodedToken.username
      const requestHeader = {
        headers: {
          Authorization: 'JWT ' + token
        }
      }

      const MY_REVIEW_URL = `http://localhost:8000/api-auth/user-reviews/${user_id}/`
      axios.get(MY_REVIEW_URL, requestHeader)
      .then((res)=>{
        console.log(res)
        this.myReviewList = res.data
      })
      .catch((e)=>{
        console.log(e)
      })
    },
  },
  mounted() {
    this.myReviews()
  },
}
</script>

<style>
</style>