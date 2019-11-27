<template>
  <div class="JustForYou mx-3">
    <h2 class="mb-4">추천영화목록</h2>
    <div class="row">
      <div v-for="(justForYou, idx) in justForYouList" :key="idx" class="card col-2 mx-2 my-2 p-0 border-0" style="width: 18rem;">
        <img :src="justForYou.image" class="card-img-top" alt="" style="height: 100%;">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'justforyou',
  props: {
    // 추천 영화 제목, 개봉일, 이미지
    justForYouList: Array
  },
  data(){
    return {
      modal_show: false
    }
  },
  components: {
  },
}
</script>

<style>
  .card-img-top {
    display: block
  }
</style>