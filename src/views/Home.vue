<template>
  <main v-if="!loading">
    <DataTilte :text="title" :dataDate="dataDate"/>

    <DataBoxes :state="stats"></DataBoxes>
  
    <CountrySelect @get-country="getCountryData" :countries="countries"/>
  </main>
  
  <main class="flex flex-col text-center justify-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="">
</main>

<button class="bg-green-700 text-white p-3 rounded focus:outline-none hover:bg-green-600 mt-10" @click="clearCountryData" v-if="stats.Country">Clear Country</button>
</template>

<script>
import DataTilte from '../components/DataTilte.vue';
import DataBoxes from '../components/DataBoxes.vue';
import CountrySelect from '../components/CountrySelect.vue';

export default {
  name: 'Home',
  components: {
    DataTilte,
    DataBoxes,
    CountrySelect
  },
  data(){
    return {
      loading: false,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif'),
    }
  },
  methods: {
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    },
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData(){
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading= false
    }
  },
  async created(){
    const data = await this.fetchCovidData()

    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  }
};
</script>
