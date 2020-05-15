<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-24 10:58:48
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-31 11:54:20
 * @Description:近七日工程运行数量柱状图
 -->
<template>
  <div id="b-histogram" style="width: 98%; height: 25vh; margin: auto;" />
</template>

<script>
// import { projectCount } from '@api/hiveCount'
import { debounce } from '../../../../utils/debounce'

export default {
  mixins: [debounce],
  data() {
    return {
      charts: '',
      histogramChartData: {
        columns: [],
        rows: []
      }
    }
  },

  created() {

  },
  destroyed() {
    clearInterval(this.timer)
  },
  mounted() {
    // this.$echarts.init(document.getElementById('b-histogram')).resize()
    this.drawLine()
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
    drawLine() {
      this.charts = this.$echarts.init(document.getElementById('b-histogram'))
      const xdata = ['05-02', '05-03', '05-04', '05-05', '05-06', '05-07', '05-08']
      const ydata = ['0', '0', '0', '0', '52', '98', '40']
      this.charts.setOption({
        color: ['#FE2279', '#00FFFF'],
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['运行总数'],
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
            },
            textStyle: {
              color: '#FFF', // 更改坐标轴文字颜色
              fontSize: 14 // 更改坐标轴文字大小
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
          axisLabel: {
            textStyle: {
              color: '#5efcfc', // 坐标的字体颜色
              fontSize: 12 // 更改坐标轴文字大小
            }
          },
          name: '工程数量',
          nameTextStyle: {
            padding: [10, 0, 0, 0], // 四个数字分别为上右下左与原位置距离
            fontSize: 12
          },
          axisTick: {
            // y轴刻度线
            show: false
          },
          axisLine: {
            show: false, // 隐藏坐标轴
            lineStyle: {
              color: '#00eeff' // 坐标轴的颜色
            }
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: '#86b1b5',
              width: 0.3
            }
          }
        },

        series: [
          {
            name: '运行总数',
            type: 'bar',
            stack: '总量',
            data: ydata,
            barWidth: 20, // 柱宽

            itemStyle: {
              normal: {
                barBorderRadius: 20,
                shadowColor: 'rgba(0, 0, 0, .2)',
                shadowBlur: 0,
                shadowOffsetY: 2,
                shadowOffsetX: 2,
                label: { show: true, position: 'top', color: '#F0F0F0' }
              }
            }
          }
        ]
      })
    },
    /**
     * 获取最近7天
     */
    getDay(date) {
      let base = new Date(date).getTime()
      const oneDay = 24 * 3600 * 1000
      const dateList = []
      // let data = [Math.random() * 300]
      const time = new Date(base)
      dateList.push(
        [
          this.doHandleMonth(time.getMonth() + 1),
          this.doHandleMonth(time.getDate())
        ].join('-')
      )
      for (let i = 1; i < 7; i++) {
        const now = new Date((base -= oneDay))
        dateList.push(
          [
            this.doHandleMonth(now.getMonth() + 1),
            this.doHandleMonth(now.getDate())
          ].join('-')
        )
      }
      const newdate = dateList.reverse()
      return newdate
    },
    /**
     * 给月份和日期加0
     */
    doHandleMonth(data) {
      let num = data
      if (num.toString().length === 1) {
        num = '0' + num
      }
      return num
    }
  }
}
</script>
