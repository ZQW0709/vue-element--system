<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-24 17:32:08
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-30 16:18:27
 * @Description:API网关情况环图
 -->
<template>
  <div id="bPie" style="width: 98%; height: 25vh; margin: auto;" />
</template>

<script>
// import { apiCount } from '@api/hiveCount'

export default {
  data() {
    return {
      charts: '',
      apiCountForm: []
    }
  },

  mounted() {
    this.drawLine('bPie')
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
      const pieData = [{ value: 0, name: '防火墙规则管理' }, { value: 1,
        name: '限速规则管理' }, { value: 21,
        name: '规则管理' }, { value: 11,
        name: '选择器管理' }, { value: 13,
        name: '接口规则管理' }]
      this.charts.setOption({
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },

        color: ['#19C1F0', '#9DCCF8', '#6EDBD2', '#8080FF'],
        series: [
          {
            color: ['#3680E1', '#53FF97', '#FD227E', '#FCF90C', '#8080FF'],
            center: ['50%', '58%'],
            name: 'API网关',
            type: 'pie',
            radius: ['60%', '80%'],
            data: pieData,
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  formatter: '{b} : {c}'
                },
                labelLine: { show: true }
              }
            }
          }
        ]
      })
    }
  }
}
</script>
