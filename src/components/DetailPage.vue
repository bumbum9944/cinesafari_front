<template>
<div class="movie-detail-page">
  <h2>{{movie.title}}</h2>
  <h4>{{movie.subtitle}}</h4>
  <div>
    <p>유저평점 : {{movie.userRating}}  관람등급 : {{movie.watchGrade}} / {{movie.showTm}}분</p>
  </div>
  <div>
    <p>| 감독 : <span v-for="director in selectedDirectors" :key="director.id">{{director.name}} | </span></p>
    <p>| 출연 |</p>
    <p v-for="actor in selectedactors" :key="actor.id">{{actor.name}}</p>
  </div>
</div>
</template>

<script>
export default {
  data(){
    return {
    }
  },
  props: {
    movie: Object
  },
  computed: {
    selectedDirectors(){
      return this.movie.directors.slice(0, 3)
    },
    selectedactors(){
      return this.movie.actors.slice(0, 10)
    },
  }
}
</script>

<style>

</style>