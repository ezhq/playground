<template>
  <div>
    <h4>IV {{ version }}</h4>
    <div id="box"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import G6 from '@antv/g6'

export default {
  name: 'Tutorial',
  components: {},
  data() {
    return {
      version: G6.Global.version,
      graph: null,
      graphData: {
        nodes: [
          { id: 'node1', x: 100, y: 200, label: 'Source', },
          { id: 'node2', x: 300, y: 200, label: 'Target', },
        ],
        edges: [
          { source: 'node1', target: 'node2', label: 'Link', },
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

      this.graph.data(this.graphData)  // 加载数据
      this.graph.render()  // 渲染数据
    },
  },
}
</script>
<style scoped>
#box {
  border: 1px solid gray;
}
</style>
