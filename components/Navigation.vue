<template>
  <div>
    <v-app-bar app dark dense color="green" fixed>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title class="d-none d-sm-block">COVID TRACKER</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn text to="/"> <v-icon left>mdi-home</v-icon> HOME </v-btn>
      <v-btn text to="about">
        <v-icon left>mdi-information</v-icon> ABOUT
      </v-btn>
      <v-btn text @click="$vuetify.theme.dark = !$vuetify.theme.dark">
        DARK <v-icon> mdi-moon-waxing-crescent</v-icon>
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer color="green" v-model="drawer" fixed temporary app>
      <v-list nav dense>
        <v-list-item-group active-class="green--text text--accent-4">
          <v-list-item v-for="link in links" :key="link">
            <v-btn
              class="drawer-btn"
              text
              :to="link == 'home' ? '/' : '/' + link"
            >
              {{ link }}
            </v-btn>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      links: ['home', 'about'],
    }
  },
}
</script>

<style scoped>
.drawer-btn {
  width: 100%;
  color: white;
}
</style>
