<template>
  <div id="app">
    <v-app id="inspire">
      <!-- ======================================================================================     -->
      <!-- ||                                                                            || -->
      <v-container fluid grid-list-sm>

        <v-layout row style="height: 70%; width: 100%;" wrap>
          <v-flex d-flex xs7 style="height: 100%; width: 100%;">
            <map-component></map-component>
          </v-flex>

          <v-flex d-flex xs5 style="height: 100%; width: 100%;">
            <bar-chart msg="prop_msg "></bar-chart>
          </v-flex>
        </v-layout>

        <v-layout row style="height: 30%; width: 100%" wrap>
          <v-flex d-flex sx12 style="height: 100%; width: 100%; background: darkgray">
              <h1>Brush zoom</h1>
          </v-flex>
        </v-layout>

      </v-container>

    </v-app>
  </div>
</template>

<script>
  import BarChart from '../components/BarChart'
  import MapComponent from '../components/MapComponent'

  export default {
  components: {
    BarChart,
    MapComponent
  }
}
</script>
