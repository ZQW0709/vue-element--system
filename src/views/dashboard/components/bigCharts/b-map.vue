<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-26 10:26:40
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-30 16:19:50
 * @Description:
 -->

<template>
  <div id="b-map" style="width: 90%; height: 50vh; margin: auto;" />
</template>

<script>
// import 'echarts/lib/component/visualMap'
import 'echarts/map/js/china.js' // 引入中国地图数据
// import { hdfsSize } from '@api/hiveCount'
// import 'echarts/map/js/lines3D.js'
export default {
  data() {
    return {
      charts: '',
      hdfsSize: ''
    }
  },

  mounted() {
    this.drawLine('b-map')
    window.addEventListener('resize', () => {
      this.debounce(() => {
        this.canvasResize()
      }, 200)()
    })
  },
  methods: {
    debounce(fn, wait = 50) {
      // 通过闭包缓存一个定时器 id
      let timer = null
      // 将 debounce 处理结果当作函数返回
      // 触发事件回调时执行这个返回函数
      return function(...args) {
        // 如果已经设定过定时器就清空上一次的定时器
        if (timer) clearTimeout(timer)
        // 开始设定一个新的定时器，定时器结束后执行传入的函数 fn
        timer = setTimeout(() => {
          fn.apply(this, args)
        }, wait)
      }
    },
    canvasResize() {
      this.charts.resize()
    },

    drawLine(id) {
      this.charts = this.$echarts.init(document.getElementById(id))
      // let size = this.hdfsSize
      this.charts.setOption({
        title: {
          text: '数据处理(GB)',
          left: 'center',
          textStyle: {
            color: '#47E1FF',
            fontSize: 30
          }
          // subtext: size,
          // subtextStyle: {
          //   color: '#47E1FF',
          //   fontSize: 40,
          // },
        },

        viewControl: {
          rotateSensitivity: 0
        },
        geo: {
          // 这个是重点配置区
          map: 'china', // 表示中国地图
          roam: true,
          layoutCenter: ['50%', '52%'],
          layoutSize: '120%',
          label: {
            normal: {
              show: true, // 是否显示对应地名
              textStyle: {
                color: '#37A2DA'
              }
            }
          },
          itemStyle: {
            normal: {
              borderColor: 'rgba(147, 235, 248, 1)',
              borderWidth: 1,
              areaColor: {
                type: 'radial',
                x: 0.5,
                y: 0.5,
                r: 0.8,
                colorStops: [
                  {
                    offset: 0,
                    color: 'rgba(147, 235, 248, 0)' // 0% 处的颜色
                  },
                  {
                    offset: 1,
                    color: 'rgba(147, 235, 248, .2)' // 100% 处的颜色
                  }
                ],
                globalCoord: false // 缺省为 false
              },
              shadowColor: 'rgba(128, 217, 248, 1)',
              // shadowColor: 'rgba(255, 255, 255, 1)',
              shadowOffsetX: -2,
              shadowOffsetY: 2,
              shadowBlur: 10
            },
            emphasis: {
              areaColor: '#389BB7',
              borderWidth: 0
            }
          }
        },

        series: [
          {
            // 白色航线特效图
            type: 'lines',

            coordinateSystem: 'geo',
            zlevel: 2, // 用于分层，z-index的效果
            effect: {
              show: true, // 动效是否显示
              period: 4, // 特效动画时间
              trailLength: 0.1, // 特效尾迹的长度
              symbol: 'arrow', // 箭头图标
              color: '#4499ee', // 特效颜色
              symbolSize: 3 // 特效大小
            },

            lineStyle: {
              normal: {
                // 正常情况下的线条样式
                color: '#FFF',
                width: 0.1, // 因为是叠加效果，要是有宽度，线条会变粗，白色航线特效不明显
                opacity: 0.5, // 尾迹线条透明度
                curveness: 0.2 // 线条曲度
              }
            },
            data: [
              {
                fromName: '福建',
                toName: '江苏',
                coords: [['119.454', '25.922'], ['119.68', '33.199']]
              },
              {
                fromName: '福建',
                toName: '安徽',
                coords: [['119.454', '25.922'], ['117.229', '31.917']]
              },
              {
                fromName: '福建',
                toName: '上海',
                coords: [['119.454', '25.922'], ['121.465', '31.289']]
              },
              {
                fromName: '福建',
                toName: '湖北',
                coords: [['119.454', '25.922'], ['114.39', '30.663']]
              },
              {
                fromName: '福建',
                toName: '南京',
                coords: [['119.454', '25.922'], [118.796252, 32.0739]]
              },
              {
                fromName: '福建',
                toName: '浙江',
                coords: [['119.454', '25.922'], ['119.531', '29.877']]
              },
              {
                fromName: '福建',
                toName: '陕西',
                coords: [['119.454', '25.922'], ['109.116', '34.2']]
              },
              {
                fromName: '福建',
                toName: '河南',
                coords: [['119.454', '25.922'], ['113.467', '34.623']]
              },
              {
                fromName: '福建',
                toName: '山东',
                coords: [['119.454', '25.922'], ['116.972', '36.737']]
              },
              {
                fromName: '福建',
                toName: '广东',
                coords: [['119.454', '25.922'], ['113.511', '23.22']]
              },
              {
                fromName: '福建',
                toName: '四川',
                coords: [['119.454', '25.922'], ['103.953', '30.762']]
              },
              {
                fromName: '福建',
                toName: '江西',
                coords: [['119.454', '25.922'], ['116.005', '28.663']]
              },
              {
                fromName: '福建',
                toName: '重庆',
                coords: [['119.454', '25.922'], ['106.438', '29.581']]
              },
              {
                fromName: '福建',
                toName: '贵州',
                coords: [['119.454', '25.922'], ['106.71', '26.564']]
              },
              {
                fromName: '福建',
                toName: '山西',
                coords: [['119.454', '25.922'], ['112.593', '37.867']]
              },
              {
                fromName: '福建',
                toName: '湖南',
                coords: [['119.454', '25.922'], ['113.082', '28.257']]
              },
              {
                fromName: '福建',
                toName: '吉林',
                coords: [['119.454', '25.922'], ['125.815', '44.258']]
              },
              {
                fromName: '福建',
                toName: '广西',
                coords: [['119.454', '25.922'], ['107.88', '22.863']]
              }
            ]
          }
        ]
      })
    }
  }
}
</script>
