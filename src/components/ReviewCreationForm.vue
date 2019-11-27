<template>
  <div class="review">
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
      }
    }
  },
  methods: {
    createReview(){
      this.$emit('createReview', this.reviewData)
      this.reviewData.content = ""
      this.reviewData.score = 0
    }
  }
}
</script>

<style>

</style>