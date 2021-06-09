<template>
  <div>
    <!--<getting-started></getting-started>-->
    <!--<tutorial></tutorial>-->
    <!--<tree-graph></tree-graph>-->
      <view-okr></view-okr>
  </div>
</template>

<script>
// @ is an alias to /src
import G6 from '@antv/g6'
import GettingStarted from './components/getting-started'
import Tutorial from './components/tutorial'
import TreeGraph from './components/treeGraph'
import viewOkr from './components/view-okr'

export default {
  name: 'G6Index',
  components: { Tutorial, GettingStarted,TreeGraph, viewOkr },
  data() {
    return {
    }
  },
  created() {
  },
  mounted() {
  },
  methods: {

  },
}
</script>
<style scoped>

</style>
