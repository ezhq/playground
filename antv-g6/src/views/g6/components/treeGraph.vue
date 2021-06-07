<template>
  <div>
    <h4>TreeGraph {{ version }}</h4>
    <hr>
    <button @click="addChildren">add children</button>
    <hr>
    <div id="box"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import G6 from '@antv/g6'

export default {
  name: 'TreeGraph',
  components: {},
  data() {
    return {
      version: G6.Global.version,
      graph: null,
      minimap: null,
      data: {
        main: null,
      },
      mock: {
        data: {
          res: {
            id: '201',
            label: "开发信息化",
            author: "谢顿",
            progress: "20",
            pre:['01'],
            parent: [],
            next: ['11', '12', '13'],
            children: [
              {
                id: '301',
                label: "开发内容信息化",
                author: "哈定",
                progress: "50",
                next: ['111'],
                children: [
                  {
                    id: '401',
                    label: "面向任务目标编程",
                    author: "迪伐斯",
                    progress: "50",
                    next: [],
                    children: [],
                  }
                ],
              },
              {
                id: '302',
                label: "持续集成信息化",
                author: "哈定",
                progress: "50",
                next: ['121'],
                children: [
                  {
                    id: '402',
                    label: "集成档案化",
                    author: "迪伐斯",
                    progress: "50",
                    next: [],
                    children: [],
                  }
                ],
              },
            ]
          }
        },
      },
    }
  },
  async created() {
  },
  async mounted() {
    await this.dataLoad()
    this.graphRegister()
    this.graphInit()
  },
  methods: {
    // 数据加载
    async dataLoad() {
      let data = this.mock.data.res

      this.data.main = data
    },


    // 注册自定义节点
    graphRegister() {
      G6.registerNode('node-main', {
        draw(cfg, group) {
          const { id, label, author, progress, next, pre } = cfg

          const configRect = {
            width: 100,
            height: 30,
            lineWidth: 1,
            fontSize: 12,
            fill: '#fff',
            radius: 4,
            stroke: 'grey',
            opacity: 1,
          }
          const configText = {
            textAlign: 'left',
            textBaseline: 'bottom',
          }
          const configNode = {
            x: -configRect.width / 2,
            y: -configRect.height / 2,
          }

          const rect = group.addShape('rect', {
            attrs: {
              x: configNode.x,
              y: configNode.y,
              ...configRect,
            },
          })

          // 名称
          group.addShape('text', {
            attrs: {
              ...configText,
              x: 12 + configNode.x,
              y: 20 + configNode.y,
              text: label.length > 6 ? label.substr(0, 6) + '...' : label,
              fontSize: 12,
              opacity: 0.85,
              fill: '#000',
              cursor: 'pointer',
            },
            name: 'node-name',
          });

          // 上一级按钮
          if (cfg.pre && cfg.pre.length) {
            const preBox = group.addShape('rect', {
              attrs: {
                x: -configRect.width/2-8,
                y: -8,
                width: 16,
                height: 16,
                stroke: 'rgba(0, 0, 0, 0.25)',
                cursor: 'pointer',
                fill: '#fff',
              },
              name: 'pre-box',
              modelId: cfg.id,
            })

            const preText = group.addShape('text', {
              attrs: {
                x:-configRect.width/2,
                y: -1,
                textAlign: 'center',
                textBaseline: 'middle',
                text: cfg.pre.length === cfg.parent.length ? '-' : '+',
                fontSize: 16,
                cursor: 'pointer',
                fill: 'rgba(0, 0, 0, 0.25)',
              },
              name: 'pre-text',
              modelId: cfg.id,
            })
          }

          // 下一级按钮
          if (cfg.next && cfg.next.length) {
            const nextBox = group.addShape('rect', {
              attrs: {
                x: configRect.width / 2 - 8,
                y: -8,
                width: 16,
                height: 16,
                stroke: 'rgba(0, 0, 0, 0.25)',
                cursor: 'pointer',
                fill: '#fff',
              },
              name: 'next-box',
              modelId: cfg.id,
            })

            const nextText = group.addShape('text', {
              attrs: {
                x: configRect.width / 2,
                y: -1,
                textAlign: 'center',
                textBaseline: 'middle',
                text: cfg.next.length === cfg.children.length ? '-' : '+',
                fontSize: 16,
                cursor: 'pointer',
                fill: 'rgba(0, 0, 0, 0.25)',
              },
              name: 'next-text',
              modelId: cfg.id,
            })
          }

          // this.drawLinkPoints(cfg, group)
          return rect
        },

      }, 'rect')
    },

    // 初始化
    graphInit() {
      // 实例化小地图
      this.minimap = new G6.Minimap({
        size: [100, 100],
        className: 'minimap',
        type: 'delegate',
      })

      // 实例化树图
      this.graph = new G6.TreeGraph({
        container: 'box',
        width: 600,
        height: 600,
        animate: true,
        fitView: true,
        // 布局
        layout: {
          type: 'mindmap',  // force:力导向 ，默认 random
          direction: 'LR',  // H V LR RL TB BT
        },
        defaultNode: {
          type: 'node-main'
        },
        defaultEdge:{
          type: 'cubic-horizontal'
        },
        // 交互
        modes: [
          {
            type: 'collapse-expand',
            onChange(item, collapsed) {
              console.log('--->onChange: item: ', item)
              const icon = item.get('group').findByClassName('collapse-icon')
              if (collapsed) {
                icon.attr('symbol', EXPAND_ICON)
              } else {
                icon.attr('symbol', COLLAPSE_ICON)
              }
            }
          },
          'drag-canvas',
          'zoom-canvas',
        ],

        // 插件
        plugins: [
          this.minimap,
        ]
      })

      // 加载
      this.graph.data(this.data.main)
      // 渲染
      this.graph.render()
    },

    // 添加子节点
    addChildren() {
      const data = {
        id: '303',
        label: "测试信息化",
        author: "市长",
        progress: "20",
        next: ['403'],
        children: [
          {
            id: '403',
            label: "Bug档案化",
            author: "骡",
            progress: "20",
          }
        ],
      }

      // this.graph.addChild(data, 'root')
      this.graph.updateChild(data, '201')
      this.graph.render()
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
