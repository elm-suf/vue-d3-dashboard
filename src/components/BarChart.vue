<template>
  <div id="app">
    <h1 style="height: 8%;">{{width}}x{{height}}</h1>

    <div id="output" ref="output">
      <svg :height="height" :width="width">
          <rect
            x="40" y="0" width="22" height="333">
          </rect>

      </svg>
    </div>
  </div>
</template>

<script>
  // import { select } from 'd3';

  export default {
  name: 'BarChart',
  props: ['msg'],
  data: () => ({
    height: 100,
    width: 250
  }),

  mounted () {
    console.log('this.$refs', this.$refs.output.getBoundingClientRect())
    const out = this.$refs.output

    this.height = out.clientHeight
    this.width = out.clientWidth

    window.addEventListener('resize', this.emitHeightValue)
  },

  watch: {
    width (oldVale, newValue) {

    }
  },
  methods: {
    emitHeightValue (some) {
      this.width = this.$refs.output.clientWidth
      this.height = this.$refs.output.clientHeight
    }
  }
}
</script>

<style scoped>

  svg {
    background: coral;
  }

  #output {
    height: 92%;
    width: 100%;
    align-items: center;
  }

  #app {
    background-color: crimson;
  }

</style>
