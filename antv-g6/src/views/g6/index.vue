<template>
  <div>
    <!--<getting-started></getting-started>-->
    <tutorial></tutorial>
  </div>
</template>

<script>
// @ is an alias to /src
import G6 from '@antv/g6'
import GettingStarted from './components/getting-started'
import Tutorial from './components/tutorial'

export default {
  name: 'G6Index',
  components: { Tutorial, GettingStarted },
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
