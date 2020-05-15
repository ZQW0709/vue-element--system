<template>
  <div>
    <ve-histogram
      :data="histogramData"
      :settings="histogramChartSettings"
      :extend="histogramChartExtend"
    ></ve-histogram>
  </div>
</template>

<script>
import Vue from 'vue'
import VeHistogram from 'v-charts/lib/histogram.common' // 柱状图
Vue.component(VeHistogram.name, VeHistogram)
export default {
  props: {
    histogramData: {
      type: Object,
      required: true,
      default: () => {
        return {
          columns: ['日期', '定时调度', '新建工程'],
          rows: [
            { 日期: '1/1', 定时调度: 0, 新建工程: 0 },
            { 日期: '1/2', 定时调度: 0, 新建工程: 0 },
            { 日期: '1/3', 定时调度: 0, 新建工程: 0 },
            { 日期: '1/4', 定时调度: 0, 新建工程: 0 },
            { 日期: '1/5', 定时调度: 0, 新建工程: 0 },
            { 日期: '1/6', 定时调度: 0, 新建工程: 0 },
            { 日期: '1/7', 定时调度: 0, 新建工程: 0 },
          ],
        }
      },
    },
  },
  data() {
    return {
      /**
       * 柱状图数据
       */
      // histogramChartData: {
      //   columns: ['日期', '定时调度', '新建工程'],
      //   rows: [
      //     { 日期: '1/1', 定时调度: 1393, 新建工程: 1093 },
      //     { 日期: '1/2', 定时调度: 3530, 新建工程: 3230 },
      //     { 日期: '1/3', 定时调度: 2923, 新建工程: 2623 },
      //     { 日期: '1/4', 定时调度: 1723, 新建工程: 1423 },
      //     { 日期: '1/5', 定时调度: 3792, 新建工程: 3492 },
      //     { 日期: '1/6', 定时调度: 4593, 新建工程: 4293 },
      //     { 日期: '1/7', 定时调度: 5201, 新建工程: 4293 },
      //   ],
      // },
      histogramChartSettings: {
        stack: { 用户: ['定时调度', '新建工程'] },
        yAxisName: ['运行工程总数'],
      },
      histogramChartExtend: {
        // color: ['#0099CC', '#0099FF'],
        color: {
          type: 'linear',
          x: 0,
          y: 0,
          x2: 0,
          y2: 1,
          colorStops: [
            {
              offset: 0,
              color: '#36D1DC', // 0% 处的颜色
            },
            {
              offset: 1,
              color: '#5B86E5', // 100% 处的颜色
            },
          ],
          globalCoord: false, // 缺省为 false
        },
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
          nameTextStyle: {
            color: 'rgb(255, 255, 255)',
            fontSize: 16,
            padding: [0, 0, 0, 50],
          },
        },
        legend: {
          show: true,
          textStyle: {
            color: 'rgb(126, 203, 224)', // 图例字体颜色
          },
        },
      },
    }
  },
}
</script>
