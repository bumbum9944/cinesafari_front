<template>
  <div class="boxoffice mx-3">
    <h2 class="mx-2">BoxOffice</h2>
    <div class="row">
      <div v-for="movie in boxOfficeList" :key="movie.id" class="col-2 mx-2 my-2 p-0">
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
  .card-img-top {
    transition: transfrom .2s;
  }
  .card-img-top:hover {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
</style>