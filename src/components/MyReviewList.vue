<template>
  <div class="my-reviwe-list">
    <div class="row">
      <div v-for="review in myReviewList" :key="review.id" class="col-3 mx-2 p-0">
        <div class="card bg-dark text-white m-2 border-0">
          <img id="myReviewCard" :src="review.image" class="card-img-top" alt="">
          <div class="card-img-overlay">
            <br>
            <br>
            <br>
            <br>
            <br>
              <p class="text-left" style="font-weight: bold; font-size: 20px;">평점 : {{review.score}}</p>
              <p style="font-weight: bold; font-size: 20px;">감상평 : {{review.content}}</p>
              <div class="" style="font-size: 20px;">
                <span data-toggle="modal" :data-target="`#movie-${review.id}`">✏️</span>
                <span @click="reviewDelete(review)">❌</span>
                </div>
          </div>
        </div>
        <ReviewUpdate :review="review" @updateReview="updateReview"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
// import jwtDecode from "jwt-decode"
import ReviewUpdate from './ReviewUpdate'
export default {
  name: "myReviewList",
  props: {
    myReviewList: Array
  },
  components: {
    ReviewUpdate
  },
  methods: {
    reviewDelete(review){
      this.$session.start()
      const token = this.$session.get('jwt')
      const reqeustHeader = {
        headers: {
          Authorization: "JWT " + token
        }
      }
      axios.delete(`http://localhost:8000/api-auth/review-delete/${review.id}/`, reqeustHeader)
      .then((res)=>{
        console.log(res)
        const targetReview = this.myReviewList.find(function(el){
          return el === review
        })
        
        const idx = this.myReviewList.indexOf(targetReview)
        if (idx > -1) {
          this.myReviewList.splice(idx, 1)
        }
      })
      .catch((e)=>{
        console.log(e)
      })
    },
    updateReview(reviewData){
      console.log(reviewData)
      this.$session.start()
      const token = this.$session.get('jwt')
      const requestHeader = {
        headers: {
          Authorization: "JWT " + token
        }
      }
      const requestForm = new FormData()
      requestForm.append('content', reviewData.content)
      requestForm.append('score', reviewData.score)

      axios.put(`http://localhost:8000/api-auth/review-update/${reviewData.review_id}/`, requestForm, requestHeader)
      .then((res)=>{
        console.log("!!!!!!!!!!!!!!")
        console.log(res)
        const targetReview = this.myReviewList.find(function(el){
          return el === reviewData.review
        })
        
        const idx = this.myReviewList.indexOf(targetReview)
        if (idx > -1) {
          this.myReviewList[idx].content = reviewData.content
          this.myReviewList[idx].score = reviewData.score
        }
      })
      .catch((e)=>{
        console.log(e)
      })
    }
  },
  mounted(){
    this.myReviewList
  }
}
</script>

<style>
#myReviewCard {
  opacity: 0.5;
}
</style>