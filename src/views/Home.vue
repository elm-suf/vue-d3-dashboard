<template>
  <div id="app">
    <v-app id="inspire">
      <!-- ======================================================================================     -->
      <!-- ||                                                                            || -->
      <v-container fluid grid-list-sm>

        <v-layout row style="height: 70%" wrap>
          <v-flex d-flex xs9>
            <v-card color="teal" dark flat tile>
              <v-card-text><h1>Map Plot here</h1></v-card-text>
            </v-card>
          </v-flex>
          <v-flex d-flex xs3>
            <v-card color="cyan" dark flat tile>
              <v-card-text><h1>BarChart here</h1></v-card-text>
              <bar-chart msg="prop_msg "></bar-chart>
            </v-card>
          </v-flex>
        </v-layout>

        <v-layout row style="height: 30%" wrap>
          <v-flex d-flex>
            <v-card color="indigo" dark flat tile>
              <v-card-text><h1>Brush zoom</h1></v-card-text>
            </v-card>
          </v-flex>
        </v-layout>

      </v-container>

    </v-app>
  </div>
</template>

<script>
  import BarChart from '../components/BarChart'

  export default {
    components: {
      BarChart
    }
  }
</script>
