<template>
  <div class="JustForYou mx-3">
    <h2 class="mx-2 mb-2">추천영화목록</h2>
    <div class="row">
      <div v-for="(justForYou, idx) in justForYouList" :key="idx" class="col-2 mx-3 my-4 p-0">
        <div class="card border-0" data-toggle="modal" :data-target="`#justForYou-${justForYou.id}`" style="height: 100%;">
          <img :src="justForYou.image" class="card-img-top" alt="">
        </div>
        <JustForYouModal :justForYou="justForYou"/>
      </div>
    </div>
  </div>
</template>

<script>
import JustForYouModal from './JustForYouModal.vue'
export default {
  name: 'justforyou',
  props: {
    // 추천 영화 제목, 개봉일, 이미지
    justForYouList: Array
  },
  components: {
    JustForYouModal
  },
  data(){
    return {
    }
  },
}
</script>

<style>
  .card-img-top {
    display: block
  }
</style>