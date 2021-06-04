<template>
  <div>
    <h4>IV {{version}}</h4>
    <div id="box"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import G6 from '@antv/g6'

export default {
  name: 'GettingStarted',
  components: {},
  data() {
    return {
      version: G6.Global.version,
      graph: null,
      graphData:{
        nodes: [
          { id: 'node1', x: 100, y: 200, },
          { id: 'node2', x: 300, y: 200, },
        ],
        edges: [
          { source: 'node1', target: 'node2', },
        ],
      },
    }
  },
  created() {
  },
  mounted() {
    this.graphInit()
  },
  methods: {
    graphInit() {
      this.graph = new G6.Graph({
        container: 'box',
        width: 500,
        height: 500,
      })

      this.graph.data(this.graphData)
      this.graph.render()
    },
  },
}
</script>
<style scoped>
#box{
  border: 1px solid gray;
}
</style>
