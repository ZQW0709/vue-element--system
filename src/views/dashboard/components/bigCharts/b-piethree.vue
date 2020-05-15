<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-24 17:32:08
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-27 14:16:14
 * @Description:数仓情况环图
 -->
<template>
  <div id="bPiethree" style="width: 98%; height: 25vh; margin: auto;" />
</template>

<script>
// import { positionsCount } from '@api/hiveCount'

export default {
  data() {
    return {
      charts: '',
      positionsCount: {},
      ringChartData: {
        columns: ['status', 'total'],
        rows: [
          { status: '已使用', total: 3530 },
          { status: '未使用', total: 2923 }
        ]
      }
    }
  },

  mounted() {
    // this.chartResize('bPiethree')
    this.drawLine('bPiethree')
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
      // console.log(this.ringChartData)
      const pieThreeData = this.ringChartData.rows

      this.charts.setOption({
        color: ['#263880'],
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },
        series: [
          {
            name: '数仓情况',
            type: 'pie',
            center: ['50%', '40%'], // 改变图表位置
            selectedMode: 'single',
            radius: ['80%', '90%'],
            label: {
              normal: {
                formatter: ' {per|{d}%} \n {b|{b}}  ', // label 的内容
                position: 'center',
                rich: {
                  // 定义不同地方的文字的字体大小和颜色

                  b: {
                    fontSize: 20,
                    color: '#5F6B7F'
                  },
                  per: {
                    fontSize: 30,
                    color: '#FFF'
                  }
                }
              }
            },

            data: [
              {
                value: pieThreeData[0].total,
                name: '磁盘占比',
                itemStyle: {
                  normal: {
                    // color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                    //   {
                    //     offset: 0,
                    //     color: '#2CECFF',
                    //   },
                    //   {
                    //     offset: 1,
                    //     color: '#21BAFF',
                    //   },
                    // ]),
                    barBorderRadius: 60,
                    shadowColor: 'rgba(0, 0, 0, .2)',
                    shadowBlur: 0,
                    shadowOffsetY: 2,
                    shadowOffsetX: 2,
                    color: {
                      type: 'linear',
                      x: 0,
                      y: 0,
                      x2: 1,
                      y2: 1,
                      colorStops: [
                        {
                          offset: 0,
                          color: '#2CECFF' // 0% 处的颜色
                        },
                        {
                          offset: 1,
                          color: '#04aaf5' // 100% 处的颜色
                        }
                      ],
                      globalCoord: false // 缺省为 false
                    }
                  }
                }
              },
              {
                value: pieThreeData[1].total,
                name: '未使用',
                label: {
                  normal: {
                    show: false
                  }
                }
              }
            ]
          }
        ]
      })
    }
  }
}
</script>
