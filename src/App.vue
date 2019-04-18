<template>
  <v-app>
    <v-navigation-drawer
      absolute
      app
      overflow
      temporary
      v-model="primaryDrawer.model">
    </v-navigation-drawer>
    <v-toolbar absolute app clipped-left>
      <v-toolbar-side-icon
        @click.stop="primaryDrawer.model = !primaryDrawer.model"
        v-if="primaryDrawer.type !== 'permanent'"
      ></v-toolbar-side-icon>
      <v-toolbar-title>Vuetify</v-toolbar-title>
    </v-toolbar>
    <v-content>
      <router-view></router-view>
    </v-content>
    <v-footer :inset="footer.inset" app>
      <span class="px-3">&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>

</template>

<script>
  import HelloWorld from './components/BarChart'

  export default {
    name: 'App',
    components: {
      HelloWorld
    },
    data: () => ({
      drawers: ['Default (no property)', 'Permanent', 'Temporary'],
      primaryDrawer: {
        model: null,
        type: 'default (no property)',
        clipped: false,
        floating: true,
        mini: false
      },
      footer: {
        inset: false
    }
    })
  }
</script>
