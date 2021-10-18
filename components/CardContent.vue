<template>
  <div>
    <h1 class="date">
      {{ cardContent.date.replace(',', ' -') }}
    </h1>
    <v-row class="mt-4">
      <v-col v-for="(val, key, index) in formattedCardContent" :key="index" cols="12" sm="6">
        <v-card
          elevation="2"
          class="d-flex flex-column justify-center align-center text-center"
        >
          <div :class="`card-styling ${val.color}`"></div>
          <v-card-title>{{ val.header }}</v-card-title>
          <v-card-text :class="`number ${val.color}--text`">
            <client-only>
              <number
                :from="parseInt(val.value * 0.25)"
                :to="val.value"
                :format="theFormat"
                :duration="parseInt(Object.keys(formattedCardContent).length-index)"
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
  computed: {
    formattedCardContent() {
      const { date, ...rest } = this.cardContent
      return rest
    }
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
