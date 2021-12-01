<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate"/>
    <DataBoxes :stats="stats"/>
    <CountrySelect @get-country="getCountryData" :countries="countries"/>
    <button @click="clearCountryData" v-if="stats.Country"
            class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">Clear Country
    </button>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-44 m-auto" alt="">
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";
import CountrySelect from "@/components/CountrySelect";

export default {
  name: 'Home',
  components: {DataTitle, DataBoxes, CountrySelect},
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/covidLoading.gif')
    }
  },
  methods: {
    async fetchCovid() {
      const response = await fetch('https://api.covid19api.com/summary')
      const data = await response.json()
      return data
    },
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData() {
      const data = await this.fetchCovid()
      this.stats = data.Global
      this.loading = false
      this.title = 'Global'
    }
  },
  async created() {
    const data = await this.fetchCovid()
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  }
}
</script>
