<template>
  <div :id="id" class="echarts-element-class">
    <div style="display: none">{{optionUpdated}}</div>
  </div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  components: { echarts },
  props: {
    options: {
      // 父组件传递的options
      type: Object,
      default: {},
    },
    id: {
      // echarts元素的id
      type: String,
      default: 'id',
    },
  },
  data() {
    return {}
  },
  computed: {
    optionUpdated() {
      this.$nextTick(() => {
        this.optionChanged(this.options)
      })
      return this.options
    },
  },
  methods: {
    resizeHander() {
      this.initEcharts(this.id).resize()
    },
    optionChanged(option) {
      this.echartsSetOption(this.id, option)
      window.addEventListener('resize', this.resizeHander) // 监听echarts图标resize事件
    },
    echartsSetOption(echart_ele_id, echart_ele_option) {
      const temp = echarts.init(document.getElementById(echart_ele_id))
      temp.clear() // echarts图表同一画布下，重新画图时 需要先清空画布缓存再执行setOption操作
      temp.setOption(echart_ele_option)
    },
    initEcharts(echart_ele_id) {
      return echarts.init(document.getElementById(echart_ele_id))
    },
  },
  beforeDestroy() {
    // 注意这里不能使用destoryed 否则无法移除window的resize事件
    window.removeEventListener('resize', this.resizeHander)
  },
}
</script>

<style lang="scss">
.echarts-element-class {
  width: 100%;
  background-color: #fff;
}
</style>
