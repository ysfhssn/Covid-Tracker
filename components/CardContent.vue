<template>
  <div>
    <h1 class="date">
      {{ cardContent.date.replace(',', ' -') }}
    </h1>
    <v-row class="mt-4">
      <v-col cols="12" sm="6">
        <v-card
          elevation="2"
          class="d-flex flex-column justify-center align-center text-center"
        >
          <div class="card-styling orange"></div>
          <v-card-title>Total Confirmed</v-card-title>
          <v-card-text class="number orange--text">
            <client-only>
              <number
                :from="parseInt(cardContent.totalConf * 0.25)"
                :to="cardContent.totalConf"
                :format="theFormat"
                :duration="4"
                easing="Power1.easeOut"
              />
            </client-only>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6">
        <v-card
          elevation="2"
          class="d-flex flex-column justify-center align-center text-center"
        >
          <div class="card-styling red"></div>
          <v-card-title>Total Deaths</v-card-title>
          <v-card-text class="number red--text">
            <client-only>
              <number
                :from="parseInt(cardContent.totalDs * 0.25)"
                :to="cardContent.totalDs"
                :format="theFormat"
                :duration="3"
                easing="Power1.easeOut"
              />
            </client-only>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row class="mt-4">
      <v-col cols="12" sm="6">
        <v-card
          elevation="2"
          class="d-flex flex-column justify-center align-center text-center"
        >
          <div class="card-styling green"></div>
          <v-card-title>Today Confirmed</v-card-title>
          <v-card-text class="number green--text">
            <client-only>
              <number
                :from="parseInt(cardContent.newConf * 0.25)"
                :to="cardContent.newConf"
                :format="theFormat"
                :duration="2"
                easing="Power1.easeOut"
              />
            </client-only>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6">
        <v-card
          elevation="2"
          class="d-flex flex-column justify-center align-center text-center"
        >
          <div class="card-styling blue"></div>
          <v-card-title>Today Deaths</v-card-title>
          <v-card-text class="number blue--text">
            <client-only>
              <number
                :from="parseInt(cardContent.newDs * 0.25)"
                :to="cardContent.newDs"
                :format="theFormat"
                :duration="1"
                easing="Power1.easeOut"
              />
            </client-only>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import Table from '~/components/Table.vue'
import CardContent from '~/components/CardContent.vue'

export default {
  props: {
    cardContent: {
      type: Object,
      required: true,
    },
  },
  methods: {
    theFormat(number) {
      return new Intl.NumberFormat().format(parseInt(number))
    },
  },
}
</script>

<style scoped>
.v-card {
  position: relative;
  overflow: hidden;
  transition: all 0.2s ease-out;
}
.v-card:hover {
  transform: scale(1.05);
}
.card-styling {
  position: absolute;
  height: 80px;
  width: 80px;
  left: -40px;
  top: -40px;
  transform: rotateZ(45deg);
}
.date,
.v-card__title {
  font-size: 1.6rem;
  font-weight: 500;
}
.v-card__text {
  font-size: 1.5rem;
}
</style>
