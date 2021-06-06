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
        nodes: [],
        edges: [],
      },
      mock: {
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
  async created() {
  },
  async mounted() {
    await this.dataLoad()
    this.graphInit()
  },
  methods: {
    async dataLoad() {
      let url = 'https://gw.alipayobjects.com/os/basement_prod/6cae02ab-4c29-44b2-b1fd-4005688febcb.json'
      const res = await fetch(url)
      const data = await res.json()
      const { nodes, edges } = data

      this.graphData.nodes = nodes
      this.graphData.edges = edges
    },
    graphInit() {
      this.graph = new G6.Graph({
        container: 'box',
        width: 1000,
        height: 800,

        fitView: true,
        fitViewPadding: [20, 40, 50, 20]
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
