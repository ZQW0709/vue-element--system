<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-25 14:15:26
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-27 15:05:33
 * @Description:
 -->
<template>
  <div id="b-radar" style="width: 98%; height: 25vh; margin: auto;" />
</template>

<script>

export default {
  data() {
    return {
      charts: '',
      // 雷达图
      radarChartData: {}
    }
  },
  mounted() {
    this.drawLine('b-radar')
    // window.addEventListener('resize', () => {
    //   this.debounce(() => {
    //     this.canvasResize()
    //   }, 200)()
    // })
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
      const countArray = [9, 4, 8, 6]
      const typeList = [
        { name: 'MYSQL', max: 12 },
        { name: 'ORACLE', max: 12 },
        { name: 'KAFKA', max: 12 },
        { name: 'HDFS', max: 12 }
      ]
      this.charts = this.$echarts.init(document.getElementById(id))
      this.charts.setOption({
        tooltip: {},
        color: ['#19C1F0', '#9DCCF8', '#6EDBD2', '#8080FF'],

        radar: {
          shape: 'circle',
          center: ['50%', '60%'],
          name: {
            textStyle: {
              color: '#fff'
            }
          },
          // splitArea: {
          //   areaStyle: {
          //     color: [
          //       'rgba(3, 92, 192, 0.1)',
          //       'rgba(3, 92, 192, 0.1)',
          //       'rgba(3, 92, 192, 0.1)',
          //       'rgba(3, 92, 192, 0.1)',
          //       'rgba(3, 92, 192, 0.1)',
          //     ], // 圆环颜色
          //     shadowColor: 'rgba(3, 92, 192)', // 圆颜色
          //     shadowBlur: 10,
          //   },
          // },
          splitArea: {
            // 圆环颜色
            areaStyle: {
              //   show:'true',
              color: ['#12294B', '#203C6E', '#12294B', '#203C6E']
            }
          },
          axisLine: {
            lineStyle: {
              color: 'rgba(3, 92, 192)' // 分割线
            }
          },
          splitLine: {
            lineStyle: {
              color: 'rgba(3, 92, 192)' // 圆线
            }
          },
          indicator: typeList
        },
        series: [
          {
            name: '数据源类型',
            type: 'radar',
            // areaStyle: {normal: {}},
            itemStyle: {
              normal: {
                label: { show: true, position: 'top', color: '#F0F0F0' }
              }
            },
            data: [
              {
                value: countArray,
                name: '数据源类型',
                areaStyle: {
                  normal: {
                    color: 'rgba(0, 255, 255, 0.8)' // 选择区域颜色
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
