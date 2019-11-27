<template>
<div class="movie-detail-page">
  <h2>{{movie.title}}</h2>
  <h4>{{movie.subtitle}}</h4>
  <div>
    <p>유저평점 : {{movie.userRating}} | 관람등급 : {{movie.watchGrade}} | {{movie.showTm}}분</p>
  </div>
  <hr>
  <div>
    <p>{{movie.description}}</p>
  </div>
  <hr>
  <div class="row">
    <div class="col-3">
      <p>| 감독 : <span v-for="director in selectedDirectors" :key="director.id">{{director.name}} | </span></p>
      <p>| 출연 |</p>
      <p v-for="actor in selectedactors" :key="actor.id">{{actor.name}}</p>
    </div>
    <div v-if="reviewList.length" :id="`carou-${movie.id}`" class="carousel slide col-9 d-flex justify-content-center my-auto" data-ride="carousel">
      <div class="carousel-item active">
        <p>작성자 : {{reviewList[0].username}}</p>
        <p>평점 : {{reviewList[0].score}}점</p>
        <p>감상평 : {{reviewList[0].content}}</p>
      </div>
      <div v-for="review in selectedreviews" :key="review.id" class="carousel-item">
        <p>작성자 : {{review.username}}</p>
        <p>평점 : {{review.score}}점</p>
        <p>감상평 : {{review.content}}</p>
      </div>
      <a class="carousel-control-prev" :href="`#carou-${movie.id}`" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
      </a>
      <a class="carousel-control-next" :href="`#carou-${movie.id}`" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
      </a>
    </div>
  </div>
</div>
</template>

<script>
// import jwtDecode from "jwt-decode"
import axios from "axios"

export default {
  name: "detailpage",
  data(){
    return {
      reviewShow: false
    }
  },
  props: {
    movie: Object,
    reviewList: Array
  },
  computed: {
    selectedDirectors(){
      return this.movie.directors.slice(0, 3)
    },
    selectedactors(){
      return this.movie.actors.slice(0, 10)
    },
    selectedreviews(){
      if (this.reviewList.length === 0){
        return null
      }
      return this.reviewList.slice(1)
    },
    // nowuser(){
    //   this.$session.start()
    //   const token = this.$session.get('jwt')
    //   return jwtDecode(token).username
    // }
  },
  methods: {
    reviewShowCheck(){
      if (this.reviewList.length === 0){
        this.reviewShow = false
      } else {
        this.reviewShow = true
      }
    },
    update(){
      
    },
    remove(review){
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
        const targetReview = this.reviewList.find(function(el){
          return el === review
        })  
        const idx = this.reviewList.indexOf(targetReview)

        if (idx > -1) {
          this.reviewList.splice(idx, 1)
        }

      })
      .catch((e)=>{
        console.log(e)
      })

    },
  },
  mounted(){
    this.reviewShowCheck()
  }
}
</script>

<style>

</style>