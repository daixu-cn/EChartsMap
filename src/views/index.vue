<template>
  <div id="china" style="width: 100%; height: 100vh"></div>
</template>
<script>
import china from "@/assets/china";
import * as echarts from "echarts";
export default {
  components: {
    echartsCom: () => import("@/components/echartsCom"),
  },
  data() {
    return {
      china,
      provincePopulation: [
        {
          name: "新疆",
          value: 2523.22,
        },
        {
          name: "青海",
          value: 607.82,
        },
        {
          name: "西藏",
          value: 350.56,
        },
        {
          name: "甘肃",
          value: 2647.43,
        },
        {
          name: "宁夏",
          value: 694.66,
        },
        {
          name: "四川",
          value: 8375,
        },
        {
          name: "云南",
          value: 4858.3,
        },
        {
          name: "贵州",
          value: 3622.95,
        },
        {
          name: "广西",
          value: 4960,
        },
        {
          name: "海南",
          value: 944.72,
        },
        {
          name: "澳门",
          value: 67.96,
        },
        {
          name: "香港",
          value: 752,
        },
        {
          name: "台湾",
          value: 2356.84,
        },
        {
          name: "福建",
          value: 3973,
        },
        {
          name: "广东",
          value: 11521,
        },
        {
          name: "浙江",
          value: 5850,
        },
        {
          name: "湖南",
          value: 6918.38,
        },
        {
          name: "湖北",
          value: 5927,
        },
        {
          name: "安徽",
          value: 6365.9,
        },
        {
          name: "江苏",
          value: 8070,
        },
        {
          name: "上海",
          value: 2428.14,
        },
        {
          name: "河南",
          value: 9640,
        },
        {
          name: "河北",
          value: 7591.97,
        },
        {
          name: "重庆",
          value: 3124.32,
        },
        {
          name: "陕西",
          value: 3876.21,
        },
        {
          name: "山西",
          value: 3729.22,
        },
        {
          name: "山东",
          value: 10070.21,
        },
        {
          name: "内蒙古",
          value: 2539.6,
        },
        {
          name: "天津",
          value: 1561.83,
        },
        {
          name: "辽宁",
          value: 4351.7,
        },
        {
          name: "吉林",
          value: 2690.73,
        },
        {
          name: "黑龙江",
          value: 3751.3,
        },
        {
          name: "江西",
          value: 4666.1,
        },
        {
          name: "南海诸岛",
          value: null,
        },
      ],
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    async initMap() {
      echarts.registerMap("china", this.china);
      let myChart = echarts.init(document.getElementById("china"));
      let chinaOption = {
        backgroundColor: "#012248",
        title: {
          show: true,
          text: "ECharts绘制中国地图",
          textStyle: {
            color: "white",
            fontSize: 30,
          },
          left: "center",
          top: 30,
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "shadow",
          },
        },
        geo: {
          //是否显示地图
          show: true,
          map: "china",
          //是否开启鼠标缩放和平移漫游
          roam: true,
          //单块区域样式
          itemStyle: {
            //正常状态下样式
            normal: {
              areaColor: "#24CFF4",
              borderColor: "#53D9FF",
              borderWidth: 1.3,
              shadowBlur: 15,
              shadowColor: "rgb(58,115,192)",
              shadowOffsetX: 7,
              shadowOffsetY: 6,
            },
            //鼠标移入状态下样式
            emphasis: {
              areaColor: "#8dd7fc",
              borderWidth: 1.6,
              shadowBlur: 25,
            },
          },
          //省份字体样式
          label: {
            //正常状态下省份字体样式
            normal: {
              show: true,
              color: "rgb(249, 249, 249)",
            },
            //鼠标移入状态下省份字体样式
            // emphasis: {
            //   show: true,
            //   color: '#f75a00',
            // },
          },
          regions: [
            // 在地图中对特定的区域配置样式。
            // {
            //   name: '青海', //区块名称
            //   itemStyle: {
            //     normal: {
            //       areaColor: '#fbd8f3',
            //     },
            //   },
            // },
          ],
          //当前视角的缩放比例。
          zoom: 1,
          // center: this.center,
        },
        //工具栏配置
        toolbox: {
          show: false,
          orient: "vertical",
          x: "right",
          y: "center",
          feature: {
            mark: { show: true },
            dataView: { show: true, readOnly: false },
            restore: { show: true },
            saveAsImage: { show: true },
          },
        },
        // visualMap: {
        //   min: 50,
        //   max: 5000,
        //   left: '3%',
        //   bottom: '5%',
        //   calculable: true,
        //   seriesIndex: [0],
        //   inRange: {
        //     color: ['#24CFF4', '#2E98CA', '#1E62AC'],
        //   },
        //   textStyle: {
        //     color: '#24CFF4',
        //   },
        // },
        series: [
          {
            type: "map",
            map: "china",
            geoIndex: 0,
            roam: true,
            zoom: 1.3,
            //提示框组件
            tooltip: {
              trigger: "item",
              backgroundColor: "rgba(50,50,50,0.5)",
              borderWidth: 0,
              textStyle: {
                color: "white",
              },
              formatter: (params) => {
                let val = params.value;
                if (!val) {
                  val = "未知";
                }
                let txtCon =
                  "<div style='text-align:left'>" +
                  params.name +
                  ":<br />当地人口：" +
                  val +
                  " (万)</div>";
                return txtCon;
              },
            },
            data: this.provincePopulation,
          },
          {
            type: "effectScatter",
            coordinateSystem: "geo",
            zlevel: 2,
            data: [
              {
                name: "百度大厦",
                value: [116.307899, 40.057038, 30],
                itemStyle: {
                  color: "#0a7ef6",
                },
              },
              {
                name: "阿里巴巴集团",
                value: [120.196358, 30.195626, 30],
                itemStyle: {
                  color: "#3fcb81",
                },
              },
              {
                name: "贵州茅台",
                value: [106.629086, 26.685695, 30],
                itemStyle: {
                  color: "#8f59e1",
                },
              },
              {
                name: "华为武汉研究所",
                value: [114.54272, 30.498025, 30],
                itemStyle: {
                  color: "#f8a505",
                },
              },
              {
                name: "兰州牛肉拉面",
                value: [103.856063, 36.059458, 30],
                itemStyle: {
                  color: "#f7476c",
                },
              },
            ],
            symbolSize: function (val) {
              return val[2] / 2;
            },
            //涟漪特效相关配置。
            rippleEffect: { brushType: "stroke" },
            hoverAnimation: true,
            //鼠标移入后改变点的位置
            emphasis: {
              itemStyle: {
                color: "yellow",
              },
              label: {
                formatter: "{b}",
                position: "right",
                show: true,
                color: "yellow",
              },
            },
            zlevel: 1,
          },
          {
            type: "lines",
            zlevel: 1,
            effect: {
              show: true,
              period: 5, //箭头指向速度，值越小速度越快
              trailLength: 0.2, //特效尾迹长度[0,1]值越大，尾迹越长重
              symbol: "arrow", //箭头图标
              symbolSize: 10, //图标大小
            },
            lineStyle: {
              normal: {
                color: "#00ffff",
                width: 3, //尾迹线条宽度
                opacity: 0.5, //尾迹线条透明度
                curveness: 0.3, //尾迹线条曲直度
              },
            },
            data: [
              [
                {
                  coord: [120.196358, 30.195626], //起始点坐标
                },
                {
                  coord: [103.856063, 36.059458], //终点坐标
                },
              ],
              [
                {
                  coord: [120.196358, 30.195626],
                },
                {
                  coord: [106.629086, 26.685695],
                },
              ],
              [
                {
                  coord: [120.196358, 30.195626],
                },
                {
                  coord: [116.307899, 40.057038],
                },
              ],
              [
                {
                  coord: [120.196358, 30.195626],
                },
                {
                  coord: [114.54272, 30.498025],
                },
              ],
            ],
          },
        ],
      };
      myChart.setOption(chinaOption);
      window.addEventListener("resize", this.resizeHanderMap);
    },
    resizeHanderMap() {
      let mapEcharts = echarts.init(document.getElementById("china"));
      mapEcharts.resize();
    },
  },
};
</script>
<style lang="scss">
body {
  margin: 0;
}
</style>