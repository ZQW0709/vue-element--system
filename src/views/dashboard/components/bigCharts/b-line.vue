<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-24 14:56:34
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-30 10:55:34
 * @Description:近24小时整体趋势折线图
 -->
<template>
  <div id="bLine" style="width: 98%;height: 25vh;margin:auto" />
</template>

<script>
export default {
  data() {
    return {
      charts: '',
      timer: '',
      histogramChartData: {
        columns: [],
        rows: []
      }
    }
  },

  mounted() {
    this.drawLine('bLine')
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

    /**
     * 获取24小时
     */
    getHour() {
      const date = new Date()
      const dateList = []
      dateList.push(this.doHandleDate(date.getHours()))
      for (let i = 1; i < 24; i++) {
        const now = new Date(date - i * 3600 * 1000)
        dateList.push(this.doHandleDate(now.getHours()))
      }
      const newdate = dateList.reverse()
      return newdate
    },
    /**
     * 给月份和日期加0
     */
    doHandleDate(data) {
      let num = data
      if (num.toString().length === 1) {
        num = '0' + num
      } else {
        num = '' + num
      }
      return num
    },
    drawLine(id) {
      this.charts = this.$echarts.init(document.getElementById(id))
      const xdata = ['18:00', '19:00', '20:00', '21:00', '22:00', '23:00', '00:00', '01:00', '02:00', '03:00', '04:00', '05:00', '06:00', '07:00', '08:00', '09:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00']
      const ydata = [6, 2, '0', '0', '0', '0', '0', '0', '0', '0', '0', '0', '0', '0', '0', 6, 11, 9, '0', 2, 19, 7, 2, 11]
      this.charts.setOption({
        color: ['#00FFFF'],
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['用户'],
          x: 'right',
          y: 'top',
          textStyle: {
            // 图例文字的样式
            color: '#FFF',
            fontSize: 16
          }
        },
        grid: {
          right: '5%',
          left: '10%',
          bottom: '11%'
        },
        xAxis: {
          type: 'category',
          data: xdata,
          // 设置轴线的属性
          axisLine: {
            lineStyle: {
              color: '#86b1b5',
              width: 0.3 // 这里是为了突出显示加上的
            }
          },
          axisLabel: {
            textStyle: {
              color: '#FAFAFA' // 坐标的字体颜色
            }
          },
          axisTick: {
            // x轴刻度线
            show: false
          }
        },
        yAxis: {
          type: 'value',

          name: '用户访问量',
          nameTextStyle: {
            padding: [10, 0, 0, 0] // 四个数字分别为上右下左与原位置距离
          },
          axisTick: {
            // y轴刻度线
            show: false
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: '#86b1b5',
              width: 0.3
            }
          },
          axisLabel: {
            textStyle: {
              color: '#5efcfc' // 坐标的字体颜色
            }
          },
          axisLine: {
            show: false, // 隐藏坐标轴
            lineStyle: {
              color: '#00eeff' // 坐标轴的颜色
            }
          }
        },

        series: [
          // {
          //   name: 'w',
          //   type: 'line',
          //   data: [120, 132, 121, 134],
          //   smooth: true, // 这个是把线变成曲线
          //   lineStyle: {
          //     normal: {
          //       // 线条阴影
          //       shadowBlur: 5,
          //       shadowColor: 'rgba(0,0,0)',
          //       shadowOffsetX: 15,
          //       shadowOffsetY: 15,
          //     },
          //   },
          // },
          {
            name: '用户',
            type: 'line',
            data: ydata,
            smooth: true, // 这个是把线变成曲线
            itemStyle: {
              normal: {
                label: { show: true, position: 'top', color: '#F0F0F0' }
              }
            },
            lineStyle: {
              normal: {
                // 线条阴影
                shadowBlur: 5,
                shadowColor: 'rgba(0,0,0)',
                shadowOffsetX: 15,
                shadowOffsetY: 15
              }
            }
          }
        ]
      })
    }
  }
}
</script>
