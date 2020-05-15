<template>
  <div>
    <ve-line
      :data="chartData"
      :settings="chartSettings"
      :extend="chartExtend"
      :grid="grid"
    ></ve-line>
  </div>
</template>

<script>
import Vue from 'vue'
import VeLine from 'v-charts/lib/line.common' // 折线图
Vue.component(VeLine.name, VeLine)
export default {
  data() {
    return {
      /**
       * 折线图配置
       */
      chartSettings: {
        stack: { 用户: ['访问用户', '下单用户'] },
        area: true,
      },

      chartData: {
        columns: ['日期', '访问用户', '下单用户'],
        rows: [
          { 日期: '1/1', 访问用户: 1393, 下单用户: 1093 },
          { 日期: '1/2', 访问用户: 3530, 下单用户: 3230 },
          { 日期: '1/3', 访问用户: 2923, 下单用户: 2623 },
          { 日期: '1/4', 访问用户: 1723, 下单用户: 1423 },
          { 日期: '1/5', 访问用户: 3792, 下单用户: 3492 },
          { 日期: '1/6', 访问用户: 4593, 下单用户: 4293 },
        ],
      },
      grid: {
        show: true,
        top: 50,
        left: 10,
        borderColor: '#000',
      },
      chartExtend: {
        color: ['#1481AF', '#13549D'],
        xAxis: {
          axisLabel: {
            textStyle: {
              color: 'rgb(255, 255, 255)', // x轴字体颜色
            },
          },
        },
        yAxis: {
          axisLabel: {
            textStyle: {
              color: 'rgb(255, 255, 255)', // y轴字体颜色
            },
          },
        },
        legend: {
          show: false,
          textStyle: {
            color: 'rgb(126, 203, 224)', // 图例字体颜色
          },
        },
        series: {
          smooth: false,
        },
      },
    }
  },
}
</script>
