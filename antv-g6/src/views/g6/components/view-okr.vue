<template>
    <!--<div class="container">-->
    <!--<button @click="addChildren">add children</button>-->
    <div id="box"></div>
    <!--</div>-->
</template>

<script>
// @ is an alias to /src
import G6 from '@antv/g6'

export default {
    name: 'viewOkr',
    components: {},
    data() {
        return {
            version: G6.Global.version,
            graph: null,
            minimap: null,
            cache: {
                focusId: 'system',
            },
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
                        pre: ['01'],
                        parent: [],
                        next: ['11', '12', '13'],
                        children: [
                            {
                                id: '301',
                                label: "开发内容信息化",
                                author: "哈定",
                                progress: "50",
                                next: ['111', '222'],
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
                api: {
                    getobjectlistbyalignfirst: {
                        "data": {
                            "logcontent": "日志内容",
                            "loguuid": "0d8c000a-bf71-11eb-9d39-00259099b30e",
                            "msgcontent": "成功或者失败原因",
                            "objectBeanList": [
                                {
                                    "alignList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "aligncount": 3,
                                    "alignedList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "alignedcount": 3,
                                    "alignstatus": 1,
                                    "kRBeanList": [
                                        {
                                            "alignstatus": 1,
                                            "krcreatetime": "5/12",
                                            "krid": 12,
                                            "krleft": 60,
                                            "krname": "会议基本功能正常使用",
                                            "krweight": 10,
                                            "taskBeanList": [
                                                {
                                                    "finishtime": "2012-01-01",
                                                    "krid": 12,
                                                    "krname": "会议基本功能正常使用",
                                                    "krweight": 10,
                                                    "okrrealname": "杨旭东",
                                                    "okrusername": "yangxudong",
                                                    "taskbegintime": "2012-12-12",
                                                    "taskendtime": "2012-12-12",
                                                    "taskid": 12,
                                                    "tasklabel": "延期4天",
                                                    "taskname": "任务内容"
                                                }
                                            ],
                                            "taskcount": 50
                                        }
                                    ],
                                    "objectid": 1,
                                    "objectleft": 80,
                                    "objectname": "视频会议持续优化",
                                    "objectstatus": "doing",
                                    "okrrealname": "李华"
                                },
                                {
                                    "alignList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "aligncount": 3,
                                    "alignedList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "alignedcount": 3,
                                    "alignstatus": 1,
                                    "kRBeanList": [
                                        {
                                            "alignstatus": 1,
                                            "krcreatetime": "5/12",
                                            "krid": 12,
                                            "krleft": 60,
                                            "krname": "会议基本功能正常使用",
                                            "krweight": 10,
                                            "taskBeanList": [
                                                {
                                                    "finishtime": "2012-01-01",
                                                    "krid": 12,
                                                    "krname": "会议基本功能正常使用",
                                                    "krweight": 10,
                                                    "okrrealname": "杨旭东",
                                                    "okrusername": "yangxudong",
                                                    "taskbegintime": "2012-12-12",
                                                    "taskendtime": "2012-12-12",
                                                    "taskid": 12,
                                                    "tasklabel": "延期4天",
                                                    "taskname": "任务内容"
                                                }
                                            ],
                                            "taskcount": 50
                                        }
                                    ],
                                    "objectid": 2,
                                    "objectleft": 40,
                                    "objectname": "标题有点长之需求开发测试上线复盘总结完善模版",
                                    "objectstatus": "doing",
                                    "okrrealname": "王刚名字也很长长长长"
                                },

                                {
                                    "alignList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "aligncount": 3,
                                    "alignedList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "alignedcount": 3,
                                    "alignstatus": 1,
                                    "kRBeanList": [
                                        {
                                            "alignstatus": 1,
                                            "krcreatetime": "5/12",
                                            "krid": 12,
                                            "krleft": 60,
                                            "krname": "会议基本功能正常使用",
                                            "krweight": 10,
                                            "taskBeanList": [
                                                {
                                                    "finishtime": "2012-01-01",
                                                    "krid": 12,
                                                    "krname": "会议基本功能正常使用",
                                                    "krweight": 10,
                                                    "okrrealname": "杨旭东",
                                                    "okrusername": "yangxudong",
                                                    "taskbegintime": "2012-12-12",
                                                    "taskendtime": "2012-12-12",
                                                    "taskid": 12,
                                                    "tasklabel": "延期4天",
                                                    "taskname": "任务内容"
                                                }
                                            ],
                                            "taskcount": 50
                                        }
                                    ],
                                    "objectid": 3,
                                    "objectleft": 10,
                                    "objectname": "objectname3",
                                    "objectstatus": "doing",
                                    "okrrealname": "谢顿"
                                },
                                {
                                    "alignList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "aligncount": 3,
                                    "alignedList": [
                                        {
                                            "okroaid": 123456,
                                            "okrrealname": "杨旭东",
                                            "okrusername": "yangxudong"
                                        }
                                    ],
                                    "alignedcount": 3,
                                    "alignstatus": 1,
                                    "kRBeanList": [
                                        {
                                            "alignstatus": 1,
                                            "krcreatetime": "5/12",
                                            "krid": 12,
                                            "krleft": 60,
                                            "krname": "会议基本功能正常使用",
                                            "krweight": 10,
                                            "taskBeanList": [
                                                {
                                                    "finishtime": "2012-01-01",
                                                    "krid": 12,
                                                    "krname": "会议基本功能正常使用",
                                                    "krweight": 10,
                                                    "okrrealname": "杨旭东",
                                                    "okrusername": "yangxudong",
                                                    "taskbegintime": "2012-12-12",
                                                    "taskendtime": "2012-12-12",
                                                    "taskid": 12,
                                                    "tasklabel": "延期4天",
                                                    "taskname": "任务内容"
                                                }
                                            ],
                                            "taskcount": 50
                                        }
                                    ],
                                    "objectid": 4,
                                    "objectleft": 75,
                                    "objectname": "objectname4",
                                    "objectstatus": "doing",
                                    "okrrealname": "赛弗哈定"
                                },
                            ],
                            "okroaid": 123456,
                            "okrrealname": "杨旭东",
                            "okrtotal": 100,
                            "okrusername": "yangxudong",
                            "result": 1
                        },
                        "downstreamInfo": {
                            "downstreamUrl": "string"
                        },
                        "encryptedData": "string",
                        "meta": {
                            "cached": false,
                            "code": 1,
                            "encrypted": false,
                            "message": "string",
                            "structure": 1
                        }
                    }
                },
            },
        }
    },
    async created() {
        this.dataMainReady()
    },
    async mounted() {
        // await this.dataLoad()
        this.graphRegister()
        this.graphInit()
    },
    methods: {
        // 从接口获取初始数据
        dataMainReady() {
            const data = JSON.parse(JSON.stringify(this.mock.api.getobjectlistbyalignfirst)).data
            // console.log('--->dataReady: data: ', data)
            this.dataMainProcess(data)
        },
        // 格式化初始数据
        dataMainProcess(inData) {
            const data = JSON.parse(JSON.stringify(inData))
            let result = {
                id: 'system',
                hide: false,
                name: 'system',
                progress: '100',
                author: 'system',
                parentExpand: false,
                parent: ['101'],
                collapsed: false,
                childrenNum: 0,
                children: [],
            }
            this.cache.focusId = result.id
            console.log('--->dataProcess: data: ', data)

            const okrs = data.objectBeanList
            okrs.forEach(okr => {
                let obj = {
                    id: String(okr.objectid),
                    hide: false,
                    name: String(okr.objectname),
                    progress: String(okr.objectleft),
                    author: String(okr.okrrealname),
                    parentExpand: false,
                    parent: [],
                    collapsed: true,
                    childrenNum: Number(okr.alignedcount),
                    children: []
                }

                result.children.push(obj)
                result.childrenNum += 1
            })
            console.log('--->dataProcess: result: ', result)
            const childrenLength = result.children.length
            if (childrenLength > 0) {
                this.cache.focusId = result.children[Math.floor(childrenLength / 2)].id
            }

            this.data.main = result
        },


        // // 数据加载
        // async dataLoad() {
        //     let data = JSON.parse(JSON.stringify(this.mock.data.res))
        //     const dataString = JSON.stringify(data)
        //     const formatDataString = dataString.replace(/progress/g, `collapsed": true, "progress`)
        //     const formatData = JSON.parse(formatDataString)
        //
        //     // console.log('--->dataLoad: data: ', data)
        //     // console.log('--->dataLoad: formatData: ', formatData)
        //
        //
        //     this.data.main = data
        // },


        // 注册
        graphRegister() {
            // 节点
            G6.registerNode('node-main', {
                draw(cfg, group) {
                    // const { id, label, author, progress, collapsed, next, pre } = cfg
                    const {
                        id,
                        hide,
                        name,
                        progress,
                        author,
                        parentExpand,
                        parent,
                        collapsed,
                        childrenNum,
                        children
                    } = cfg

                    const configRect = {
                        width: 256,
                        height: 91,
                        lineWidth: 0,
                        fontSize: 12,
                        fill: '#fff',
                        radius: 6,
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

                    // 背景矩形
                    const rect = group.addShape('rect', {
                        attrs: {
                            x: configNode.x,
                            y: configNode.y,
                            ...configRect,
                            shadowColor: 'rgba(0, 0, 0, 0.04)',
                            shadowBlur: 4,
                            shadowOffsetX: 0,
                            shadowOffsetY: 2,
                        },
                    })

                    // 名称
                    group.addShape('text', {
                        attrs: {
                            ...configText,
                            x: 15 + configNode.x,
                            y: 35 + configNode.y,
                            text: name.length > 15 ? name.substr(0, 14) + '...' : name,
                            fontSize: 15,
                            opacity: 1,
                            fill: '#333',
                            cursor: 'pointer',
                        },
                        name: 'node-name',
                    });

                    // 进度条背景
                    const progressRectBack = group.addShape('rect', {
                        attrs: {
                            x: 15 + configNode.x,
                            y: 49 + configNode.y,
                            width: 186,
                            height: 5,
                            fill: '#f3f3f3',
                            radius: 2.5,
                        },
                        name: 'progress-rect-back'
                    });

                    // 进度条前景
                    const progressRectFront = group.addShape('rect', {
                        attrs: {
                            x: 15 + configNode.x,
                            y: 49 + configNode.y,
                            width: Number(progress) / 100 * 186,
                            height: 5,
                            fill: '#df3031',
                            radius: 2.5,
                        },
                        name: 'progress-rect-front'
                    });

                    // 进度条文字
                    const progressText = group.addShape('text', {
                        attrs: {
                            x: progressRectBack.getBBox().maxX + 5,
                            y: progressRectBack.getBBox().maxY + 2.5,
                            text: `${progress}%`,
                            fontSize: 12,
                            textAlign: 'left',
                            textBaseline: 'bottom',
                            lineHeight: 17,
                            opacity: 1,
                            fill: '#333',
                            cursor: 'pointer',
                        },
                        name: 'progress-text',
                    });

                    // 上一级按钮
                    if (parent.length > 0) {
                        const preBox = group.addShape('rect', {
                            attrs: {
                                x: -configRect.width / 2 - 8,
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
                                x: -configRect.width / 2,
                                y: -1,
                                textAlign: 'center',
                                textBaseline: 'middle',
                                text: parentExpand ? '-' : '+',
                                fontSize: 16,
                                cursor: 'pointer',
                                fill: 'rgba(0, 0, 0, 0.25)',
                            },
                            name: 'pre-text',
                            modelId: cfg.id,
                        })
                    }

                    // 下一级按钮
                    if (childrenNum > 0) {
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
                            modelId: id,
                        })

                        const nextText = group.addShape('text', {
                            attrs: {
                                x: configRect.width / 2,
                                y: -1,
                                textAlign: 'center',
                                textBaseline: 'middle',
                                // text: progress,
                                // text: childrenExpand ? `${childrenNum}` : '+',
                                text: collapsed ? String(childrenNum) : "-",
                                fontSize: 16,
                                cursor: 'pointer',
                                fill: 'rgba(0, 0, 0, 0.25)',
                            },
                            name: 'next-text',
                            modelId: id,
                        })
                    }

                    // 作者背景
                    const authorRectBack = group.addShape('rect', {
                        attrs: {
                            x: 15 + configNode.x,
                            y: 60 + configNode.y,
                            width: 12 + (author.length) * 12,
                            height: 17,
                            fill: '#f2f2f2',
                            radius: 9,
                        },
                        name: 'author-rect-back'
                    });

                    // 作者文字
                    const authorText = group.addShape('text', {
                        attrs: {
                            x: 21 + configNode.x,
                            y: 76 + configNode.y,
                            text: author,
                            fontSize: 12,
                            textAlign: 'left',
                            textBaseline: 'bottom',
                            lineHeight: 17,
                            opacity: 1,
                            fill: '#666',
                            cursor: 'pointer',
                        },
                        name: 'author-text',
                    });


                    // this.drawLinkPoints(cfg, group)
                    return rect
                },

                setState(name, value, item) {
                    // console.log('--->setState: name: ', name)
                    // console.log('--->setState: value: ', value)
                    // console.log('--->setState: item: ', item)
                    const nodeData = item._cfg.model
                    console.log('--->setState: nodeData: ', nodeData)

                    if (name === 'collapsed') {
                        const group = item.getContainer()
                        const nextText = group.find(e => e.get('name') === 'next-text')
                        // console.log('--->setState: group: ', group)
                        // console.log('--->setState: nextText: ', nextText)

                        if (nextText) {
                            if (!value) {
                                nextText.attr({
                                    text: '-'
                                })
                            } else {
                                nextText.attr({
                                    // text: '+'
                                    text: `${item._cfg.model.childrenNum}`
                                })
                            }
                        }
                    }
                },

            }, 'rect')

            // 边
            G6.registerEdge(
                'flow-cubic',
                {
                    getControlPoints(cfg) {
                        let controlPoints = cfg.controlPoints; // 指定controlPoints
                        if (!controlPoints || !controlPoints.length) {
                            const { startPoint, endPoint, sourceNode, targetNode } = cfg;
                            const { x: startX, y: startY, coefficientX, coefficientY } = sourceNode
                                ? sourceNode.getModel()
                                : startPoint;
                            const { x: endX, y: endY } = targetNode ? targetNode.getModel() : endPoint;
                            let curveStart = (endX - startX) * coefficientX;
                            let curveEnd = (endY - startY) * coefficientY;
                            curveStart = curveStart > 40 ? 40 : curveStart;
                            curveEnd = curveEnd < -30 ? curveEnd : -30;
                            controlPoints = [
                                { x: startPoint.x + curveStart, y: startPoint.y },
                                { x: endPoint.x + curveEnd, y: endPoint.y },
                            ];
                        }
                        return controlPoints;
                    },
                    getPath(points) {
                        const path = [];
                        path.push(['M', points[0].x, points[0].y]);
                        path.push([
                            'C',
                            points[1].x,
                            points[1].y,
                            points[2].x,
                            points[2].y,
                            points[3].x,
                            points[3].y,
                        ]);
                        return path;
                    },
                },
                'single-line',
            );

            // 交互
            G6.registerBehavior('node-touch', {
                getEvents() {
                    return {
                        'node:touchend': 'onTouchEnd'
                    }
                },
                onTouchEnd(e) {
                    const node = e.target.cfg
                    const nodeId = node.modelId
                    const nodeName = node.name
                    console.log(`--->onTouchEnd: e: nodeId: ${nodeId} | nodeName: ${nodeName}`)

                    if (!!nodeId) {
                        const idNextButton = nodeName.includes('next-')
                        const isPreButton = nodeName.includes('pre-')


                        const item = this.graph.findById(nodeId)
                        const nodeModel = item.getModel()
                        nodeModel.collapsed = !nodeModel.collapsed

                        this.graph.layout()
                        this.graph.setItemState(item, 'collapsed', nodeModel.collapsed)
                    }

                },
            })
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
            const box = document.getElementById('box')
            const boxWidth = box?.scrollWidth || 600
            const boxHeight = box?.scrollHeight || 600

            this.graph = new G6.TreeGraph({
                container: 'box',
                width: boxWidth,
                height: boxHeight,
                animate: true,
                // fitView: true,
                defaultZoom: 1.0,
                // 布局
                layout: {
                    type: 'mindmap',  // force:力导向 ，默认 random
                    direction: 'LR',  // H V LR RL TB BT
                    getHGap: e => 152,
                    getVGap: e => 45,
                },
                // 节点
                defaultNode: {
                    type: 'node-main'
                },
                // 边
                defaultEdge: {
                    type: 'cubic-horizontal'
                },
                // 交互
                modes: {
                    default: [

                        'drag-canvas',
                        'zoom-canvas',
                        'node-touch',


                        // {
                        //     type: 'collapse-expand',
                        //     onChange(item, collapsed) {
                        //         console.log('--->onChange: item: ', item)
                        //         const icon = item.get('group').findByClassName('collapse-icon')
                        //         if (collapsed) {
                        //             icon.attr('symbol', EXPAND_ICON)
                        //         } else {
                        //             icon.attr('symbol', COLLAPSE_ICON)
                        //         }
                        //     }
                        // },
                    ],
                },


                // 插件
                plugins: [
                    // this.minimap,
                ]
            })

            // 加载
            console.log('--->graphInit: data.main: ', this.data.main)
            this.graph.data(this.data.main)

            // 渲染
            this.graph.render()

            // 隐藏节点
            this.graph.getNodes().forEach(node => {
                const model = node._cfg.model
                const hide = !!model.hide
                if (hide) {
                    this.graph.hideItem(node)
                }
            })

            // 聚焦节点
            this.focusItemById()

            // 监听
            const nextClick = e => {
                const id = e.target.get('modelId')
                const item = this.graph.findById(id)
                const nodeModel = item.getModel()
                nodeModel.collapsed = !nodeModel.collapsed

                console.log('--->nextClick: graph: ', this.graph)
                console.log('--->nextClick: nodeModel: ', nodeModel)

                this.graph.layout()
                this.graph.setItemState(item, 'collapsed', nodeModel.collapsed)
            }
            this.graph.on('next-text:click', e => {
                nextClick(e)
            })
            this.graph.on('next-box:click', e => {
                nextClick(e)
            })
        },

        // 聚焦节点
        focusItemById(inId = this.cache.focusId) {
            const id = inId
            const item = this.graph.findById(id)
            this.graph.focusItem(item, true, {
                easing: 'easeLinear',
                duration: 400,
            });
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
            this.graph.layout()
        },
    },
}
</script>
<style scoped>
#box {
    height: 100%;
    border: 2px solid deepskyblue;
    background-color: #f5f5f5;
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
