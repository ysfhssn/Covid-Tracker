<template>
  <v-app dark>
    <Navigation></Navigation>

    <!-- MAIN CONTENT -->
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <!-- ------------ -->

    <Footer></Footer>
  </v-app>
</template>

<script>
import Footer from '~/components/Footer.vue'
import Navigation from '@/components/Navigation.vue'

export default {
  components: {
    Navigation,
    Footer,
  },
}
</script>
