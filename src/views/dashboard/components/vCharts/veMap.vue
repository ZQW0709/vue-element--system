<template>
  <div class="echarts">
    <div ref="myEchart" :style="{ height: '520px', width: '100%' }" />
  </div>
</template>
<script>
// import echarts from 'echarts'
import 'echarts/lib/component/visualMap'
import 'echarts/map/js/china.js' // 引入中国地图数据
// import { hdfsSize } from '@api/hiveCount'
export default {
  data() {
    return {
      chart: null,
      hdfsSize: ''
    }
  },
  mounted() {
    this.getHdfsSize()
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    async getHdfsSize() {
      const res = await hdfsSize()
      this.hdfsSize = res.item.hdfsSize
      this.initEchartMap()
    },
    initEchartMap() {
      const myChart = this.$echarts.init(this.$refs.myEchart)

      const keys = Object.keys(this.hdfsSize)[0]
      const size = this.hdfsSize[keys]

      window.onresize = myChart.resize
      myChart.setOption({
        title: {
          text: '数据处理(' + keys + ')',
          left: 'center',
          textStyle: {
            color: '#47E1FF',
            fontSize: 30
          },
          subtext: size,
          subtextStyle: {
            color: '#47E1FF',
            fontSize: 30
          }
        },
        tooltip: {
          trigger: 'item'
        },
        visualMap: {
          show: true,
          min: 0,
          max: 2000,
          calculable: true,
          dimension: 0,
          inRange: {
            color: ['#B1DEE4', '#96CDD2', '#82BEC6', '#5F9BA6', '#437D89']
          },
          outOfRange: {
            color: ['red']
          },
          textStyle: {
            color: '#12223b'
          }
        },
        viewControl: {
          rotateSensitivity: 0
        },
        geo: {
          // 这个是重点配置区
          map: 'china', // 表示中国地图
          color: 'red',
          roam: true,
          layoutCenter: ['50%', '50%'],
          layoutSize: '130%',
          label: {
            normal: {
              show: true, // 是否显示对应地名
              textStyle: {
                color: 'rgba(0,0,0)'
              }
            }
          },
          itemStyle: {
            color: 'red',
            normal: {
              // areaColor: '#B1DEE4', // 区域颜色
              borderColor: '#FFF',
              borderWidth: 1,
              shadowColor: '#FFF'
            }
          }
        },
        series: [
          {
            name: '浏览量',
            type: 'map',
            roam: true,
            coordinateSystem: 'geo',
            zlevel: 1, // 用于分层，z-index的效果
            geoIndex: 0,
            label: {
              normal: {
                formatter: '{b}',
                position: 'right',
                show: false
              },
              emphasis: {
                show: true
              }
            },
            data: [
              { name: '北京', value: Math.round(Math.random() * 2000) },
              { name: '天津', value: Math.round(Math.random() * 2000) },
              { name: '上海', value: Math.round(Math.random() * 2000) },
              { name: '重庆', value: Math.round(Math.random() * 2000) },
              { name: '河北', value: Math.round(Math.random() * 2000) },
              { name: '河南', value: Math.round(Math.random() * 2000) },
              { name: '云南', value: Math.round(Math.random() * 2000) },
              { name: '辽宁', value: Math.round(Math.random() * 2000) },
              { name: '黑龙江', value: Math.round(Math.random() * 2000) },
              { name: '湖南', value: Math.round(Math.random() * 2000) },
              { name: '安徽', value: Math.round(Math.random() * 2000) },
              { name: '山东', value: Math.round(Math.random() * 2000) },
              { name: '新疆', value: Math.round(Math.random() * 2000) },
              { name: '江苏', value: Math.round(Math.random() * 2000) },
              { name: '浙江', value: Math.round(Math.random() * 2000) },
              { name: '江西', value: Math.round(Math.random() * 2000) },
              { name: '湖北', value: Math.round(Math.random() * 2000) },
              { name: '广西', value: Math.round(Math.random() * 2000) },
              { name: '甘肃', value: Math.round(Math.random() * 2000) },
              { name: '山西', value: Math.round(Math.random() * 2000) },
              { name: '内蒙古', value: Math.round(Math.random() * 2000) },
              { name: '陕西', value: Math.round(Math.random() * 2000) },
              { name: '吉林', value: Math.round(Math.random() * 2000) },
              { name: '福建', value: Math.round(Math.random() * 2000) },
              { name: '贵州', value: Math.round(Math.random() * 2000) },
              { name: '广东', value: Math.round(Math.random() * 2000) },
              { name: '青海', value: Math.round(Math.random() * 2000) },
              { name: '西藏', value: Math.round(Math.random() * 2000) },
              { name: '四川', value: Math.round(Math.random() * 2000) },
              { name: '宁夏', value: Math.round(Math.random() * 2000) },
              { name: '海南', value: Math.round(Math.random() * 2000) },
              { name: '台湾', value: Math.round(Math.random() * 2000) },
              { name: '香港', value: Math.round(Math.random() * 2000) },
              { name: '澳门', value: Math.round(Math.random() * 2000) }
            ]
          },
          {
            // 白色航线特效图
            type: 'lines',
            zlevel: 2, // 用于分层，z-index的效果
            effect: {
              show: true, // 动效是否显示
              period: 6, // 特效动画时间
              trailLength: 0.7, // 特效尾迹的长度
              color: '#4499ee', // 特效颜色
              symbolSize: 3 // 特效大小
            },

            lineStyle: {
              normal: {
                // 正常情况下的线条样式
                color: 'red',
                width: 1, // 因为是叠加效果，要是有宽度，线条会变粗，白色航线特效不明显
                curveness: 0.2 // 线条曲度
              }
            },
            data: [
              {
                fromName: '福建',
                toName: '江苏',
                value: 4000,
                coords: [['119.454', '25.922'], ['119.68', '33.199']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '安徽',
                value: 4000,
                coords: [['119.454', '25.922'], ['117.229', '31.917']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '上海',
                value: 4000,
                coords: [['119.454', '25.922'], ['121.465', '31.289']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '湖北',
                value: 4000,
                coords: [['119.454', '25.922'], ['114.39', '30.663']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '南京',
                value: 4000,
                coords: [['119.454', '25.922'], [118.796252, 32.0739]],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '浙江',
                value: 4000,
                coords: [['119.454', '25.922'], ['119.531', '29.877']]
              },
              {
                fromName: '福建',
                toName: '陕西',
                value: 4000,
                coords: [['119.454', '25.922'], ['109.116', '34.2']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '河南',
                value: 4000,
                coords: [['119.454', '25.922'], ['113.467', '34.623']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '山东',
                value: 4000,
                coords: [['119.454', '25.922'], ['116.972', '36.737']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '广东',
                value: 4000,
                coords: [['119.454', '25.922'], ['113.511', '23.22']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '四川',
                value: 4000,
                coords: [['119.454', '25.922'], ['103.953', '30.762']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '江西',
                value: 4000,
                coords: [['119.454', '25.922'], ['116.005', '28.663']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '重庆',
                value: 4000,
                coords: [['119.454', '25.922'], ['106.438', '29.581']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '贵州',
                value: 4000,
                coords: [['119.454', '25.922'], ['106.71', '26.564']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '山西',
                value: 4000,
                coords: [['119.454', '25.922'], ['112.593', '37.867']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '湖南',
                value: 4000,
                coords: [['119.454', '25.922'], ['113.082', '28.257']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '吉林',
                value: 4000,
                coords: [['119.454', '25.922'], ['125.815', '44.258']],
                visualMap: false
              },
              {
                fromName: '福建',
                toName: '广西',
                value: 4000,
                coords: [['119.454', '25.922'], ['107.88', '22.863']],
                visualMap: false
              }
            ]
          }
        ]
      })
    }
  }
}
</script>
