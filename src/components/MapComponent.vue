<template>
  <div class="hello">
    <div ref="mapoutput" style="height: 100%;">
      <!--      <div style="position:absolute;">-->
      <!--&lt;!&ndash;        <h1>{{width}}x{{height}}</h1>&ndash;&gt;-->
      <!--        <v-btn v-for="(item, key) in projections" :key="key" @click="selected(item)">{{key}}</v-btn>-->
      <!--      </div>-->

      <svg :height="height" :width="width" class="binded" viewBox="256 32 400 400">
        <g class="group">
          <path :d="generatePath" class="sphere"></path>
          <path
            :d="generator(count)"
            :key="index"
            @click="countryClicked(count)"
            class="land"
            v-for="(count , index) in countries.features"
          >
            <title>{{detailInfo[count.id]}}</title>
          </path>
        </g>
      </svg>
    </div>
  </div>
</template>
<script>
  import { event, geoMercator, geoPath, json, select, tsv, zoom } from 'd3'
  import { geoAzimuthalEqualArea, geoNaturalEarth1, geoTransverseMercator } from 'd3-geo'
  import { feature } from 'topojson'

  export default {
  name: 'MapComponent',
  data () {
    return {
      projection: geoNaturalEarth1(),
      projections: {
        geoMercator: geoMercator(),
        geoAzimuthalEqualArea: geoAzimuthalEqualArea(),
        geoNaturalEarth1: geoNaturalEarth1(),
        geoTransverseMercator: geoTransverseMercator()
      },
      countries: {},
      detailInfo: {},
      width: 0,
      height: 0
    }
  },
  mounted () {
    const out = this.$refs.mapoutput

    this.height = out.clientHeight
    this.width = out.clientWidth

    window.addEventListener('resize', this.emitHeightValue)
    console.log('created')

    tsv('https://unpkg.com/world-atlas@1.1.4/world/50m.tsv').then(ddd => {
      ddd.forEach(el => {
        this.detailInfo[el.iso_n3] = el.name
      })
    })

    json('https://unpkg.com/world-atlas@1.1.4/world/50m.json').then(data => {
      this.countries = feature(data, data.objects.countries)
    })

    select('svg').call(zoom().on('zoom', function () {
      // console.log('zooming', this)
      select('.group').attr('transform', event.transform)
    }))
  },

  watch: {},
  computed: {
    generator () {
      return geoPath().projection(this.projection)
    },
    generatePath () {
      return this.generator({ type: 'Sphere' })
    }
  },
  methods: {
    countryClicked (count) {
      console.log('count', count)
    },
    selected (item) {
      console.log('SELECTED', item)
      this.projection = item
    },
    emitHeightValue (event) {
      console.log(event)
      this.width = this.$refs.mapoutput.clientWidth
      this.height = this.$refs.mapoutput.clientHeight
    }
  }
}
</script>

<style scoped>
  .sphere {
    background: #200491;
    fill: #200491;
  }

  svg {
    background: #2c3e50;
  }

  path {
    margin: 200px;
    fill: #42b983;
    stroke: rgb(88, 45, 45);
    stroke-width: 0.5px;
  }

  .land:hover {
    fill: crimson;
  }

  rect {
    fill: red;
  }
</style>
