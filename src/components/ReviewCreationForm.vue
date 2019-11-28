<template>
  <div class="review">
    <div v-if="errors.length" class="error-list alert alert-danger">
        <div v-for="(error, idx) in errors" :key="idx">{{error}}</div>
    </div>
    <div class="review-input-group">
      <input type="text" class="form-control mt-2" v-model="reviewData.content">
      <input type="number" class="form-control mt-2" min="1" max="10" v-model="reviewData.score">
      <button class="btn btn-outline-light mt-2" @click="createReview" @keydown.enter="createReview">리뷰작성</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ReviewCreationForm",
  data(){
    return {
      reviewData: {
        content: "",
        score: 0
      },
      errors: []
    }
  },
  methods: {
    createReview(){
      if (this.checkForm()) {        
        this.$emit('createReview', this.reviewData)
        this.reviewData.content = ""
        this.reviewData.score = 0
      }
    },
    checkForm(){
      this.errors = []
      if (this.reviewData.content.length === 0) {
        this.errors.push("내용을 입력해주세요.")
      }
      if (!this.reviewData.score) {
        this.errors.push("평점을 입력해주세요.")
      }
      if (this.errors.length === 0) {
        return true
      }
    }
  }
}
</script>

<style>

</style>