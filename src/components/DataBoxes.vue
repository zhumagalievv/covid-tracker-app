<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!--  Box1 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">
        Cases
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">
          New:   {{ numberWithCommas(stats.NewConfirmed) }}
        </span>
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">
          Total: {{ numberWithCommas(stats.TotalConfirmed) }}
        </span>
      </div>
    </div>
    <!--  Box2  -->
    <div class="shadow-md bg-blue-200 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">
        Deaths
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">
          New: {{ numberWithCommas(stats.NewDeaths) }}
        </span>
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">
          Total: {{ numberWithCommas(stats.TotalDeaths) }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ['stats'],
  methods: {
    numberWithCommas(number) {
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
    }
  }
}
</script>

<style scoped>

</style>