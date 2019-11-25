<template>
  <div class="box-office-detail">
    <div class="modal fade" tabindex="-1" role="dialog" :id="`movie-${movie.boxoffice}`" data-backdrop="static" data-keyboard="false">
      <div class="modal-dialog modal-xl" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <BasicPage v-show="basic" :movie="movie"/>
            <DetailPage v-show="detail" :movie="movie"/>
            <SimilarPage v-show="similar" :movie="movie"/>
          </div>
          <div class="modal-footer">
            <div>
              <button @click="basicPage">
                기본정보
              </button>
              <button @click="detailPage">
                상세보기
              </button>
              <button @click="similarPage">
                비슷한영화
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import $ from 'jquery';
import BasicPage from "../components/BasicPage"
import DetailPage from "../components/DetailPage"
import SimilarPage from "../components/SimilarPage"
export default {
  props: {
    movie: Object
  },
  components: {
    BasicPage,
    DetailPage,
    SimilarPage
  },
  data(){
    return {
      basic: true,
      detail: false,
      similar: false,
    }
  },
  methods: {
    basicPage(){
      this.basic = true
      this.detail = false
      this.similar = false
    },
    detailPage(){
      this.basic = false
      this.detail = true
      this.similar = false
    },
    similarPage(){
      this.basic = false
      this.detail = false
      this.similar = true
    }
  },
  
}
</script>

<style>

</style>