<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-24 17:32:08
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-30 14:57:54
 * @Description:算子种类饼图
 -->
<template>
  <div id="bPietwo" style="width: 98%; height: 25vh; margin: auto;" />
</template>

<script>

export default {
  data() {
    return {
      charts: '',
      pieChartData: []
    }
  },

  mounted() {
    this.drawLine('bPietwo')
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
      // const Pietwodata = [{ name: '预处理',
      //   value: 10 }, { name: 'spark算子',
      //   value: 15 }]
      this.charts.setOption({
        color: ['#19C1F0', '#9DCCF8', '#6EDBD2', '#8080FF'],
        grid: {
          left: 0, // 与容器左侧的距离
          right: 0, // 与容器右侧的距离
          top: 0, // 与容器顶部的距离
          bottom: 20 // 与容器底部的距离
        },
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },
        // legend: {
        //   y: 'bottom',
        //   orient: 'horizontal',
        //   data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎'],
        //   textStyle: {
        //     // 图例文字的样式
        //     color: '#FFF',
        //     fontSize: 10,
        //   },
        // },
        series: [
          {
            name: '算子种类',
            type: 'pie',
            center: ['50%', '60%'], // 改变图表位置
            selectedMode: 'single',
            radius: [0, '70%'],

            // label: {
            //   position: 'inner',
            // },
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  formatter: '{b} : {c} '
                },
                labelLine: { show: true }
              }
            },
            labelLine: {
              show: true
            },

            data: [{ name: '预处理',
              value: 10 }, { name: 'spark算子',
              value: 15 }, { name: '数据预处理',
              value: 6 }, {
              name: '实时算子',
              value: 8
            }],
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: 'rgba(0, 0, 0, 0.5)'
              }
            }
          }
        ]
      })
    }
  }
}
</script>
