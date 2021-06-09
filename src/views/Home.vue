<template>
  <main v-if="!loading">
    <data-title :text="title" :dataDate="dataDate" />
    <data-boxes :stats="stats" />
    <country-select @get-country="GetCountryData" :countries="countries" />
    <button @click="ClearCountryData"
    v-if="stats.Country"
    class="bg-green-700 text-white rounded p-3 mt-5 focus:outline-none hover:bg-green-600">
      Clear Country
    </button>
  </main>
  <main v-else class="flex flex-col align-center justify-center
  text-center">
  <div class="text-grey-500 text-3xl mt-10 mb-6">
    Fetching Data
  </div>
  <img :src="loadngImage" class="w-24 m-auto" alt="">

  </main>
</template>

<script>
import axios from 'axios'
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'
import CountrySelect from '@/components/CountrySelect'
export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect

  },
  data(){
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadngImage: require('../assets/hrGlass.gif')
    }
  },
  methods: {
    // fetchCovidData(){
    //        axios.get('https://api.covid19api.com/summary')
    //        .then((response)=>{
    //     this.details = response.data.countries
    //   })
    //   .catch((error)=>{
    //     console.log(error);
    //     this.errorMsg = 'Error retriving data';
    //   })
      
    // },
    async fetchCovidData(){
        const res = await fetch('https://api.covid19api.com/summary')
        const data = await res.json()
        return data
    },
    GetCountryData(country){
      this.title = country.Country
      this.stats = country
    },
    async ClearCountryData(){
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading = false
    },
  },
   async created(){
     const data = await this.fetchCovidData()
     this.dataDate = data.Date
     this.stats = data.Global
     this.countries = data.Countries
     this.loading = false
  },
  
}
</script>
