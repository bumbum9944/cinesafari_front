<template>
  <div class="home">
    <BoxOffice :boxOfficeList = "boxOfficeList"/>
    <div class="mt-5">
      <JustForYou/>
    </div>
  </div>
</template>

<script>
import BoxOffice from '../components/BoxOffice.vue'
import JustForYou from '../components/JustForYou.vue'
import axios from 'axios'

export default {
  name: 'home',
  data(){
    return {
      boxOfficeList: []
    }
  },
  components: {
    BoxOffice,
    JustForYou
  },
  methods: {
    boxOffice(){
      const BOXOFFICE_URL = 'http://localhost:8000/api-auth/boxoffice/'
      axios.get(BOXOFFICE_URL)
      .then((res)=>{
        console.log(res)
        // this.boxOfficeList = res.data.boxOfficeResult.weeklyBoxOfficeList
        this.boxOfficeList = res.data
      })
      .catch((e)=>{
        console.log(e)
      })
    }
  },
  mounted() {
    this.boxOffice()
  }
}
</script>
