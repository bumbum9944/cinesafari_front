<template>
  <div class="boxoffice mx-3">
    <h2 class="mx-2 mb-2">BoxOffice</h2>
    <div class="row">
      <div v-for="movie in boxOfficeList" :key="movie.id" class="col-2 mx-2 p-0">
        <div class="card m-2 border-0">
          <img :src="movie.image" class="card-img-top" data-toggle="modal" :data-target="`#movie-${movie.boxoffice}`" alt="">
        </div>
        <BoxOfficeModal :movie="movie"/>
      </div>
    </div>
  </div>
</template>

<script>
import BoxOfficeModal from './BoxOfficeModal.vue'
export default {
  name: "boxoffice",
  data(){
    return {
      modal_show: false
    }
  },
  props: {
    boxOfficeList: Array,
  },
  components: {
    BoxOfficeModal
  },
}
</script>

<style>
  .card-img-top {
    display: block
  }
</style>