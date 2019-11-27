<template>
  <div class="review-udate">
    <div class="modal fade" tabindex="-1" role="dialog" :id="`movie-${review.id}`" data-keyboard="false">
      <div class="modal-dialog modal-xl" role="document">
        <div class="modal-content text-white" style="background-color: black;">
          <div class="modal-body">
            <div>
              <input type="text" class="form-control mt-2" v-model="reviewData.content">
              <input type="number" class="form-control mt-2" min="1" max="10" v-model="reviewData.score">
              <button type="button" class="close text-light" style="font-size: 30px;" data-dismiss="modal" aria-label="Close" @click="updateReview">
                리뷰수정
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    review: Object
  },
  components: {
    
  },
  data(){
    return {
      reviewData: {
        content: this.review.content,
        score: this.review.score,
        review_id: this.review.id,
        review: this.review
      }
    }
  },
  methods: {
    updateReview(){
      this.$emit('updateReview', this.reviewData)
    }
  }
}
</script>

<style>

</style>