<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-25 14:15:26
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-30 16:31:33
 * @Description:数据异常类型(个)大屏条形图
 -->
<template>
  <div id="b-bar" style="width: 98%; height: 25vh; margin: auto;" />
</template>

<script>

export default {

  data() {
    return {
      charts: '',
      barChartData: {
        rows: [],
        colums: []
      }
    }
  },

  mounted() {
    this.drawLine('b-bar')
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
      const xdata = ['3', '15', '2', '4', '3', '1', '0']
      const ydata = ['非空性检测', '值域有效性检测', '正则规则检测', '唯一性检测', '关联一致性检测', '枚举检测', '未知异常']
      this.charts.setOption({
        color: {
          type: 'linear',
          x: 0,
          y: 0,
          x2: 1,
          y2: 1,
          colorStops: [
            {
              offset: 0,
              color: '#3C78F1' // 0% 处的颜色
            },
            {
              offset: 1,
              color: '#47e1ff' // 100% 处的颜色
            }
          ],
          globalCoord: false // 缺省为 false
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },

        grid: {
          left: '3%',
          right: '6%',
          bottom: '3%',
          top: '20%',
          containLabel: true
        },
        xAxis: {
          type: 'value',
          // boundaryGap: [0, 0.01],   // 坐标轴空白策略
          // max:xMax,

          // 设置轴线的属性
          axisLine: {
            show: false, // 隐藏坐标轴
            lineStyle: {
              color: '#FFF',
              width: 1 // 这里是为了突出显示加上的
            },
            textStyle: {
              color: '#FFF', // 更改坐标轴文字颜色
              fontSize: 14 // 更改坐标轴文字大小
            }
          },
          axisTick: {
            // x轴刻度线
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
              color: '#FAFAFA', // 坐标的字体颜色
              fontSize: 12 // 更改坐标轴文字大小
            }
          }
        },
        yAxis: {
          type: 'category',
          name: '类型',
          nameTextStyle: {
            padding: [-30, 0, 0, 0] // 四个数字分别为上右下左与原位置距离
          },
          axisTick: {
            // 刻度线
            show: false
          },

          data: ydata,
          axisLabel: {
            textStyle: {
              color: '#FFF' // 坐标的字体颜色
            }
          },
          axisLine: {
            show: false, // 隐藏坐标轴
            lineStyle: {
              color: '#FFF' // 坐标轴的颜色
            }
          }
        },
        series: [
          {
            name: '数量',
            type: 'bar',
            barWidth: 10, // 柱宽
            itemStyle: {
              normal: {
                // barBorderRadius: 20,
                barBorderRadius: [0, 20, 20, 0],
                shadowColor: 'rgba(0, 0, 0, .2)',
                shadowBlur: 0,
                shadowOffsetY: 2,
                shadowOffsetX: 2
              }
            },
            label: {
              normal: {
                show: true,
                position: 'right',
                color: '#F0F0F0'
              }
            },
            data: xdata
          }
        ]
      })
    }
  }
}
</script>
