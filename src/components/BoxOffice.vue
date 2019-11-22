<template>
  <div class="boxoffice mx-3">
    <h2 class="mb-4">BoxOffice</h2>
    <div class="row">
      <div v-for="(movie, idx) in boxOfficeList" :key="idx" class="card col-2 m-2">
        <img :src="movie.image" class="card-img-top" alt="">
        <div class="card-body">
          <h5 class="card-title">{{movie.movieNm}}</h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    boxOfficeList: Array
  }
}
</script>

<style>
  .card-img-top {
    display: block
  }
</style>