<template>
  <div class="hello">
    <h2>Demo Scatter Plot</h2>
    <!--    <input placeholder="emoji" type="text">-->
    <button @click="someClick">click</button>

    <div id="chart_output">
      <svg viewBox="0 0 1000 1000" :height="h" :width="w" class="blank" id="canvas">
        <circle
          :cx="xScale(item.c1)"
          :cy="yScale(item.c2)"
          :key="i"
          :r="3"
          :fill="color(item.out)"
          v-for="(item, i) in dataset"
        >
          <title>{{item}}</title>
        </circle>
      </svg>
    </div>
  </div>
</template>

<script>
  import { axisBottom, axisRight, interpolateHcl, json, scaleBand, scaleLinear, select, Selection } from 'd3'

  export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      w: 1000,
      h: 1000,
      dataset: [],
      xAx: Selection,
      yAx: Selection,
      xPadding: 32,
      yPadding: 32,
      emojis: [],
      dict: {}
    }
  },
  mounted () {
    // this.w = document.getElementById('chart_output').clientWidth
    // this.h = document.getElementById('chart_output').clientHeight
    window.addEventListener('resize', this.emitHeightValue)

    // csv('https://vizhub.com/curran/datasets/auto-mpg.csv').then(loadedData => {
    //   this.dataset = loadedData
    // })

    json('https://raw.githubusercontent.com/matiassingers/emoji-flags/master/data.json')
      .then(d => {
        this.emojis = d
        d.forEach(el => {
          this.dict[el.code] = el.emoji
        }
        )
      })

    json('http://localhost:3000/inandout')
      .then(d => {
        this.dataset = d
        this.xAx = select('#canvas')
          .append('g')
          .call(this.xAxis)
        this.yAx = select('#canvas')
          .append('g')
          .call(this.yAxis)
          // .attr('transform', 'translate(10,10)')
        // .exit().remove();

        console.log(this.color(0))
        console.log(this.color(3904))

      })
  },
  computed: {
    xAxis () {
      return axisBottom()
        .scale(this.xScale)
      // .tickLabels(this.emojis, d => d.emoji)
        .tickValues(this.xScale.domain()
          .filter((d, i) => !(i % 2)))
        .tickFormat(d => this.dict[d])
    },
    yAxis () {
      return axisRight()
        .scale(this.yScale)
        .tickValues(this.yScale.domain()
          .filter((d, i) => !(i % 4)))
        .tickFormat(d => this.dict[d])
    },
    yScale () {
      return scaleBand()
        .domain(this.emojis.map(el => el.code))
        .range([0, this.h])
    },
    xScale () {
      return scaleBand()
        .domain(this.emojis.map(el => el.code))
        .range([0, this.w])
    },
    color () {
      return scaleLinear()
        .domain([0, 3904])
        .range(["brown", "steelblue"])
        .interpolate(interpolateHcl);
        // .domain([0, 3904])
        // .range(['#f7f4f9', '#7f00ff'])
    }
  },
  watch: {
    // w (oldValue, newValue) {
    //   this.xAx.remove()
    //   this.xAx = select('#canvas')
    //     .append('g')
    //     .call(this.xAxis)
    //   console.log(oldValue, newValue)
    // }
  },
  methods: {
    // emitHeightValue (some) {
    //   this.w = document.getElementById('chart_output').clientWidth
    // },
    someClick (some) {
      console.log(this.xScale.domain())
      console.log(this.dict['GB'])
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  circle {
    /*fill: crimson;*/
    /* stroke: rgb(6, 133, 63); */
    opacity: 0.5;
    transition: all 0.5s ease;
  }

  circle:hover {
    fill: rgb(6, 133, 63);
    stroke: crimson;
    opacity: 1;
    transition: all 1s ease;
    r: 32;
  }

  .hello {
    border: 0.1em solid red;
    overflow: hidden;
  }

  .blank {
    background: #ae9eff;
  }

  .chart {
    background: black;
  }
</style>
