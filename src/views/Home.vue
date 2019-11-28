<template>
  <div class="home">
    <BoxOffice :boxOfficeList="boxOfficeList"/>
    <div class="mt-5">
      <JustForYou :justForYouList="justForYouList"/>
    </div>
  </div>
</template>

<script>
import jwtDecode from "jwt-decode"
import BoxOffice from '../components/BoxOffice.vue'
import JustForYou from '../components/JustForYou.vue'
import axios from 'axios'


export default {
  name: 'home',
  data(){
    return {
      boxOfficeList: [],
      justForYouList: [],
      user_id: 1,
      intervalid1: '',
      intervalid2: ''
    }
  },
  props: {
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
    },
    justForYou(){
      if (this.$session.has('jwt')){
      this.$session.start()
      const token = this.$session.get('jwt')
      const decodedToken = jwtDecode(token)
      this.user_id = decodedToken.user_id
      }
      
      const FORYOU_URL = `http://localhost:8000/api-auth/recommand/${this.user_id}/`
      axios.get(FORYOU_URL)
      .then((res)=>{
        // this.boxOfficeList = res.data.boxOfficeResult.weeklyBoxOfficeList
        this.justForYouList = res.data
      })
      .catch((e)=>{
        console.log(e)
      })
    },
  },
  mounted() {
    this.boxOffice()
    this.justForYou()
  },
  updated(){
  this.justForYou()
  }
}
</script>