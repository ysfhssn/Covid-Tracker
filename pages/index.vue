<template>
  <div class="main mt-5">
    <CardContent :cardContent="cardContent" />
    <Table
      class="mt-16"
      :dataArray="topTen"
      :dataHeaders="[
        'Country',
        'Total Deaths',
        'TotalConfirmed',
        'Today Deaths',
        'Today Confirmed',
      ]"
    />

    <h1 class="mt-16 text-center font-weight-medium">
      Most affected countries
    </h1>
    <client-only>
      <BarChart
        class="mt-4"
        v-if="$vuetify.theme.dark || this.$vuetify.breakpoint.smAndDown"
        :data="data"
        :options="options"
      />
      <BarChart
        v-else
        key="666"
        class="mt-4"
        :data="data"
        :options="options"
      />
    </client-only>
  </div>
</template>

<script>
import Table from '~/components/Table.vue'
import CardContent from '~/components/CardContent.vue'

export default {
  async asyncData({ $axios, error }) {
    try {
      const url = 'https://api.covid19api.com/summary'
      const data = await $axios.$get(url)
      const global = data.Global
      console.log(global)
      const cardContent = {
        date: new Date(global.Date).toLocaleString('fr-FR'),
        totalConf: global.TotalConfirmed,
        totalDs: global.TotalDeaths,
        newConf: global.NewConfirmed,
        newDs: global.NewDeaths,
      }
      let countriesData = data.Countries
      countriesData.sort((a, b) => b.TotalDeaths - a.TotalDeaths)
      const topTen = countriesData.slice(0, 10)

      return {
        cardContent,
        topTen,
      }
    } catch (e) {
      error({ statusCode: e.response.status })
    }
  },
  computed: {
    data() {
      return {
        labels: this.topTen.map((item) =>
          item.Country.length > 10 ? item.CountryCode : item.Country
        ),
        datasets: [
          {
            backgroundColor: this.getRandomColors(10),
            data: this.topTen.map((item) => item.TotalDeaths),
          },
        ],
      }
    },
    options() {
      return {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          yAxes: [
            {
              scaleLabel: {
                display: true,
                labelString: 'Total Deaths',
                fontSize: 16,
                fontColor: this.$vuetify.theme.dark ? 'white' : 'black',
              },
              ticks: {
                padding: 18,
                beginAtZero: true,
                fontColor: this.$vuetify.theme.dark ? 'white' : 'black',
              },
              gridLines: {
                color: this.$vuetify.theme.dark ? 'white' : 'black',
                zeroLineColor: this.$vuetify.theme.dark ? 'white' : 'black',
                drawBorder: false,
              },
            },
          ],
          xAxes: [
            {
              ticks: {
                padding: 5,
                maxRotation: this.$vuetify.breakpoint.smAndDown ? 90 : 0,
                minRotation: this.$vuetify.breakpoint.smAndDown ? 90 : 0,
                fontColor: this.$vuetify.theme.dark ? 'white' : '',
              },
              gridLines: {
                display: false,
              },
            },
          ],
        },
        legend: {
          display: false,
        },
      }
    },
  },
  methods: {
    getRandomColor() {
      let letters = '0123456789ABCDEF'
      let color = '#'
      for (let i = 0; i < 6; i++)
        color += letters[Math.floor(Math.random() * 16)]
      return color
    },
    getRandomColors(num) {
      let arr = []
      for (let i = 0; i < num; i++) {
        const color = this.getRandomColor()
        arr.push(color)
      }
      return arr
    },
  },
}
</script>
