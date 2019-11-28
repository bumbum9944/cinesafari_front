<template>
  <div class="similar-movie">
    <div class="row">
      <div v-for="similar in similarList" :key="similar.id" class="col-2 mx-2 my-2 p-0">
        <div class="card m-2 border-0 text-center" style="background-color: #343536;">
          <img :src="similar.image" class="card-img-top" alt="">
            <h5 class="card-title mt-2">{{similar.title}}</h5>
            <p class="card-text">{{similar.watchGrade}} | {{similar.showTm}}분</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "similarMovie",
  props: {
    similarList: Array
  }
}
</script>

<style>

</style>