<template>
  <div class="movie-similar-page">
    <h1>이 영화들은 어떠세요</h1>
    <SimilarMovie :similarList="similarList"/>
  </div>
</template>

<script>
import SimilarMovie from './SimilarMovie.vue'
export default {
  name: "similarPage",
  props: {
    similarList: Array
  },
  components: {
    SimilarMovie
  },

}
</script>

<style>

</style>