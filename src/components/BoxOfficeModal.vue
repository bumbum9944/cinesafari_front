<template>
  <div class="box-office-detail">
    <div class="modal fade" tabindex="-1" role="dialog" :id="`movie-${movie.boxoffice}`" data-keyboard="false">
      <div class="modal-dialog modal-xl" role="document">
        <div class="modal-content text-white" style="background-color: black;">
          <div class="modal-header">
            <button type="button" class="close text-light" style="font-size: 30px;" data-dismiss="modal" aria-label="Close" @click="closing">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class=img-cover-div><img :src="movie.thumbnail" alt=""></div>
            <div class="content">
              <BasicPage v-show="basic" :movie="movie"/>
              <DetailPage v-show="detail" :movie="movie" :reviewList="reviewList"/>
              <SimilarPage v-show="similar" :movie="movie"/>
              <ReviewCreationForm class="review-create" v-show="review" @createReview="createReview"/>
              <button type="button" v-show="reviewButton" class="btn btn-outline-light" @click="reviewPage">리뷰쓰기</button>
            </div>
          </div>
          <div class="modal-footer">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button type="button" class="btn btn-outline-light" @click="basicPage">기본정보</button>
              <button type="button" class="btn btn-outline-light" @click="detailPage">상세보기</button>
              <button type="button" class="btn btn-outline-light" @click="similarPage">비슷한영화</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import jwtDecode from "jwt-decode"
// import $ from 'jquery';
import BasicPage from "../components/BasicPage.vue"
import DetailPage from "../components/DetailPage.vue"
import SimilarPage from "../components/SimilarPage.vue"
import ReviewCreationForm from "../components/ReviewCreationForm.vue"
export default {
  name: "boxofficemodal",
  props: {
    movie: Object,
  },
  components: {
    BasicPage,
    DetailPage,
    SimilarPage,
    ReviewCreationForm
  },
  data(){
    return {
      basic: true,
      detail: false,
      similar: false,
      review: false,
      reviewList: [],
      reviewButton: true
    }
  },
  methods: {
    basicPage(){
      this.basic = true
      this.detail = false
      this.similar = false
      this.review = false
      this.reviewButton = true
      
    },
    detailPage(){
      this.basic = false
      this.detail = true
      this.similar = false
      this.review = false
      this.reviewButton = true
    },
    similarPage(){
      this.basic = false
      this.detail = false
      this.similar = true
      this.review = false
      this.reviewButton = true
    },
    reviewPage(){
      this.review = true
      this.basic = false
      this.detail = false
      this.similar = false
      this.reviewButton = false
    },
    closing(){
      this.basic = true
      this.detail = false
      this.similar = false
      this.review = false
    },
    createReview(reviewData){
      this.review = false
      this.basic = false
      this.detail = true
      this.similar = false
      this.reviewButton = true
      this.$session.start()
      const token = this.$session.get('jwt')
      const decodedToken = jwtDecode(token)
      const user_id = decodedToken.user_id
      const requestHeader = {
        headers: {
          Authorization: 'JWT ' + token
        }
      }

      const requestForm = new FormData()
      requestForm.append('user', user_id)
      requestForm.append('movie', this.movie.id)
      requestForm.append('content', reviewData.content)
      requestForm.append('score', reviewData.score)

      axios.post('http://localhost:8000/api-auth/review-create/', requestForm, requestHeader)
      .then((res)=>{
        // console.log(res)
        this.reviewList.push(res.data)
      })
      .catch((e)=>{
        console.log(e)
      })
    },
    getReviews(){
      this.$session.start()
      const token = this.$session.get('jwt')
      const requestHeader = {
        header: {
          Authoriztion: 'JWT ' + token
        }
      }

      axios.get(`http://localhost:8000/api-auth/reviews/${this.movie.id}/`, requestHeader)
      .then((res)=>{
        // console.log(res)
        this.reviewList = res.data
      })
      .catch((e)=>{
        console.log(e)
      })
      this.review = false
      this.basic = false
      this.detail = true
      this.similar = false
    }
  },
  mounted(){
    this.getReviews()
  },
  updated(){
    
  }
}
</script>

<style>
img {
  height: 100%;
  width: 100%;
}
.modal-body {
  position: relative;
  height: 90vh;
}
.modal-footer {
  z-index: 2;
}
.img-cover-div {
  opacity: 0.6;
  z-index: 1;
}

.content {
  position: absolute;
  top: 5%;
  z-index: 2;
}
.review-create {
  top: 50%;
  left: 50%;
}
</style>