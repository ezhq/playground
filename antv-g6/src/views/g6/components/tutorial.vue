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
      minimap: null,
      imageMinimap: null,
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

        // 交互
        modes: {
          default: [
            'drag-canvas',
            'zoom-canvas',
            'drag-node',
            {
              type: 'tooltip',
              formatText(model) {
                return 'label: ' + model.label + '<br/>class: ' + model.class
              },
            },
            {
              type: 'edge-tooltip',
              formatText(model) {
                return `source: ${model.source}<br/>target: ${model.target}<br/>weight: ${model.weight}`
              }
            },
          ], // 默认模式
          edit: [], // 编辑模式
        },

        // 节点状态
        nodeState: {
          hover: {
            fill: 'lightsteelblue',
          },
          click: {
            stroke: '#000',
            lineWidth: 3,
          },
        },

        // 边状态
        edgeState: {
          click: {
            stroke: 'steelblue',
          }
        },

        // 小地图
        minimap: {
          size: [100, 100],
          className: 'minimap',
          type: 'delegate',
        },
        imageMinimap: {
          width: 200,
          graphImg: 'https://gw.alipayobjects.com/mdn/rms_f8c6a0/afts/img/A*eD7nT6tmYgAAAAAAAAAAAABkARQnAQ',
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
      this.minimap = new G6.Minimap(this.config.minimap)
      // this.imageMinimap = new G6.Minimap(this.config.imageMinimap)
      this.graph = new G6.Graph({
        container: 'box',
        width: 1000,
        height: 800,
        animate: true,

        // 布局
        // fitView: true,
        // fitViewPadding: [20, 40, 50, 20],
        layout: this.config.layout, // 布局配置，执行 render() 时候进行计算
        // 节点
        defaultNode: this.config.node,
        // 边
        defaultEdge: this.config.edge,
        // 交互
        modes: this.config.modes,
        // 状态
        nodeStateStyles: this.config.nodeState,
        edgeStateStyles: this.config.edgeState,
        // 插件
        plugins: [
          this.minimap,
          // this.imageMinimap
        ]

      })

      // 加载
      this.graph.data(this.graphData)
      // 渲染
      this.graph.render()

      // 鼠标移入节点
      this.graph.on('node:mouseenter', e => {
        const item = e.item
        this.graph.setItemState(item, 'hover', true)
      })
      // 鼠标移出节点
      this.graph.on('node:mouseleave', e => {
        const item = e.item
        this.graph.setItemState(item, 'hover', false)
      })
      // 鼠标点击节点
      this.graph.on('node:click', e => {
        const nodes = this.graph.findAllByState('node', 'click')
        nodes.forEach(item => this.graph.setItemState(item, 'click', false))
        const node = e.item
        this.graph.setItemState(node, 'click', true)
      })
      // 鼠标点击边
      this.graph.on('edge:click', e => {
        const edges = this.graph.findAllByState('edge', 'click')
        edges.forEach(item => this.graph.setItemState(item, 'click', false))
        const edge = e.item
        this.graph.setItemState(edge, 'click', true)
      })

      // 更新图片缩略图
      // this.imageMinimap.updateGraphImage('https://gw.alipayobjects.com/mdn/rms_f8c6a0/afts/img/A*y8u6Rrc78uIAAAAAAAAAAABkARQnAQ')
    },
  },
}
</script>
<style>
#box {
  border: 1px solid gray;
}
.g6-tooltip {
  border: 1px solid #e2e2e2;
  border-radius: 4px;
  font-size: 12px;
  color: #545454;
  background-color: rgba(255, 255, 255, 0.9);
  padding: 10px 8px;
  box-shadow: rgb(174, 174, 174) 0 0 10px;
}
</style>
