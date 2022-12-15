<template>
  <v-app class="font-family-montserrat-default app">
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="mini"
      :clipped="clipped"
      absolute
      app
    >
    </v-navigation-drawer>

    <v-app-bar
      :clipped-left="clipped"
      app
      absolute
      elevation="0"
      dark
      clipped-right
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>

    <v-main app>
      <div class="full-height-app">
        <nuxt />
      </div>
    </v-main>

    <!--v-navigation-drawer
      app
      fixed
      clipped
      right
      width="400"
    >
      <ui-toolbar title="Окошечко" divider>
        <v-spacer></v-spacer>
        <v-btn icon>
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </ui-toolbar>
    </v-navigation-drawer-->
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'AdminLayout',
  components: {},
  data: () => ({
    title: 'SDO PROF',
    clipped: true,
    drawer: true,
    fixed: false,
    mini: false,
  }),
  computed: {},
})
</script>

<style scoped>
.app {
  max-width: 1500px; /* 1500px */
  margin: 0 auto;
}
</style>
