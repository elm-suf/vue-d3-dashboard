<template>
  <div id="app">
    <!-- ======================================================================================     -->
    <!-- ||                                                                            || -->
    <v-container fluid grid-list-sm>
      <h1>{{msg}}WORKS</h1>
    </v-container>

  </div>
</template>

<script>
  export default {
    props: ['msg'],
    data: () => ({})
  }
</script>

<style scoped>

  svg {
    background: cadetblue;
  }

</style>
