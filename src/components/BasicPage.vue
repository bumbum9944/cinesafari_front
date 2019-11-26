<template>
  <div class="movie-basic-page">
    <h2>{{movie.title}}</h2>
    <h4>{{movie.subtitle}}</h4>
    <div>
      <p>유저평점 : {{movie.userRating}} {{movie.watchGrade}} / {{movie.showTm}}분</p>
    </div>
    <hr>
    <div>
      <p>{{movie.descript_point}}</p>
    </div>
    <hr>
    <div>
      <p>| 감독 : <span v-for="director in selectedDirectors" :key="director.id">{{director.name}} | </span></p>
      <p>| 출연 : <span v-for="actor in selectedactors" :key="actor.id">{{actor.name}} | </span></p>
      <p>| 장르 : <span v-for="genre in movie.genres" :key="genre.id">{{genre.name}} | </span></p>
    </div>
  </div>
</template>

<script>
export default {
  name: "basicpage",
  props: {
    movie: Object
  },
  computed: {
    selectedDirectors(){
      // console.log(this.movie)
      return this.movie.directors.slice(0, 1)
    },
    selectedactors(){
      return this.movie.actors.slice(0, 3)
    },
  }
}
</script>

<style>

</style>