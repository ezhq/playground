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
      config: {
        // 节点
        node: {
          size: 30,  // 大小

          style: {
            fill: 'steelblue',
            stroke: '#666',
            lineWidth: 1,
          },

          labelCfg: {
            style: {
              fill: '#fff',
            },
          },
        },

        // 边
        edge: {
          // style: {
          //   opacity: 0.6,
          //   stroke: 'grey'
          // },
          labelCfg: {
            autoRotate: true,
          }
        },

        // 布局
        layout: {
          type: 'force',  // force:力导向 ，默认 random
          preventOverlap: true,  // 防止节点重叠
          // nodeSize: 30,  // 节点大小，未设置节点时候设置此项防止重叠
          linkDistance: 100, // 边长度
        },
      },
      graphData: {
        nodes: [],
        edges: [],
      },
      mock: {
        graphConfig: {
          nodes: {},
          edges: {},
        },
        graphData: {
          nodes: [],
          edges: [],
        },

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
      // 数据
      let url = 'https://gw.alipayobjects.com/os/basement_prod/6cae02ab-4c29-44b2-b1fd-4005688febcb.json'
      const res = await fetch(url)
      const data = await res.json()
      const { nodes, edges } = data
      console.log('--->dataLoad: nodes: ', nodes)

      // 节点样式
      nodes.forEach(node => {
        if (!node.style) {
          node.style = {}
        }

        switch (node.class) {
          case 'c0':
            node.type = 'circle'
            break
          case 'c1':
            node.type = 'rect'
            node.size = [35, 20]
            break
          case 'c2':
            node.type = 'ellipse'
            node.size = [35, 20]
            break
        }
      })

      // 边线样式
      edges.forEach(edge => {
        if (!edge.style) {
          edge.style = {}
        }

        edge.style.lineWidth = edge.weight
        edge.style.opacity = 0.6
        edge.style.stroke = 'grey'
      })

      // 数据
      this.graphData.nodes = nodes
      this.graphData.edges = edges
    },
    graphInit() {
      this.graph = new G6.Graph({
        container: 'box',
        width: 1000,
        height: 800,

        // 布局
        // fitView: true,
        // fitViewPadding: [20, 40, 50, 20],
        layout: this.config.layout, // 布局配置，执行 render() 时候进行计算
        defaultNode: this.config.node,
        defaultEdge: this.config.edge,
      })

      // 加载
      this.graph.data(this.graphData)
      // 渲染
      this.graph.render()
    },
  },
}
</script>
<style scoped>
#box {
  border: 1px solid gray;
}
</style>
