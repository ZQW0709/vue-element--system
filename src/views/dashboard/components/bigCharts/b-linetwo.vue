<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-24 14:56:34
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-30 16:06:28
 * @Description:数据处理量折线图
 -->
<template>
  <div id="bLinetwo" style="width: 98%;height: 25vh;margin:auto" />
</template>

<script>

export default {
  data() {
    return {
      charts: '',
      trendCountData: {
        colums: [],
        rows: []
      }
    }
  },

  mounted() {
    this.drawLine('bLinetwo')
    window.addEventListener('resize', () => {
      this.debounce(() => {
        this.canvasResize()
      }, 200)()
    })
  },

  // mounted() {
  //   //
  //   // 实现自适应部分
  //   window.addEventListener('resize', () => {
  //     this.$echarts.init(document.getElementById('bLinetwo')).resize()
  //   })
  // },
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
      const xData = ['05-09', '05-10', '05-11', '05-12', '05-13', '05-14', '05-15']
      const yData = ['5', '8', '10', '6', '6', '25', '6']
      this.charts.setOption({
        color: ['#FD227E'],
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['数据处理量'],
          x: 'right',
          y: 'top',
          textStyle: {
            // 图例文字的样式
            color: '#FFF',
            fontSize: 16
          }
        },
        grid: {
          top: '20%',
          right: '5%',
          left: '11%',
          bottom: '11%'
        },
        xAxis: {
          type: 'category',
          data: xData,
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
          axisTick: {
            // y轴刻度线
            show: false
          },
          name: '数量',
          nameTextStyle: {
            padding: [10, 0, 0, 0] // 四个数字分别为上右下左与原位置距离
          },
          type: 'value',
          axisLabel: {
            textStyle: {
              color: '#5efcfc' // 坐标的字体颜色
            },
            formatter: '{value}W'
          },

          splitLine: {
            show: true,
            lineStyle: {
              color: '#86b1b5',
              width: 0.3
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
          {
            name: '数据处理量',
            type: 'line',
            data: yData,
            smooth: true, // 这个是把线变成曲线
            itemStyle: {
              // 显示数值
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
