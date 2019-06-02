<template>
  <v-app>
    <v-navigation-drawer absolute app overflow temporary
      v-model="primaryDrawer.model">
      <v-list>
        <v-list-tile
          :key="item.name"
          :to="item.path"
          v-for="item in items"
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>

          <v-list-tile-content>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>

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
  </v-app>

</template>

<script>

  export default {
  name: 'App',
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
    },
    items: [
      { title: 'Dashboard', path: '/', icon: 'dashboard' },
      { title: 'About', path: '/about', icon: 'info' },
      { title: 'Map', path: '/map', icon: 'place' },
      { title: 'ScatterPlot', path: '/scatter', icon: 'place' },
    ]
  })
}
</script>
