<template>
  <div>
    <ve-bar
      :data="barData"
      :settings="barChartSettings"
      :extend="barchartExtend"
    ></ve-bar>
  </div>
</template>

<script>
import Vue from 'vue'
import VeBar from 'v-charts/lib/bar.common' // 条形图
Vue.component(VeBar.name, VeBar)

export default {
  props: {
    barData: {
      type: Object,
      required: true,
      default: () => {
        return {
          columns: ['类型', '数量'],
          rows: [
            { 类型: '枚举性', 数量: 1393 },
            { 类型: '关联一致性', 数量: 3530 },
            { 类型: '正则规则', 数量: 2923 },
            { 类型: '值域有效性', 数量: 1723 },
            { 类型: '唯一性问题', 数量: 3792 },
            { 类型: '非空性问题', 数量: 4593 },
          ],
        }
      },
    },
  },
  data() {
    return {
      /**
       * 条形图 */
      // barChartData: {
      //   columns: ['类型', '访问用户', '下单用户', '下单率'],
      //   rows: [
      //     { 类型: '枚举性', 访问用户: 1393, 下单用户: 1093, 下单率: 0.32 },
      //     { 类型: '关联一致性', 访问用户: 3530, 下单用户: 3230, 下单率: 0.26 },
      //     { 类型: '正则规则', 访问用户: 2923, 下单用户: 2623, 下单率: 0.76 },
      //     { 类型: '值域有效性', 访问用户: 1723, 下单用户: 1423, 下单率: 0.49 },
      //     { 类型: '唯一性问题', 访问用户: 3792, 下单用户: 3492, 下单率: 0.323 },
      //     { 类型: '非空性问题', 访问用户: 4593, 下单用户: 4293, 下单率: 0.78 },
      //   ],
      // },
      barChartSettings: {
        dimension: ['类型'],
        metrics: ['数量'],
        itemStyle: {
          normal: {},
        },
      },
      barchartExtend: {
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
        color: {
          type: 'linear',
          x: 0,
          y: 0,
          x2: 0,
          y2: 1,
          colorStops: [
            {
              offset: 0,
              color: '#3C78F1', // 0% 处的颜色
            },
            {
              offset: 1,
              color: '#47e1ff', // 100% 处的颜色
            },
          ],
          globalCoord: false, // 缺省为 false
        },
        series: {
          smooth: false,
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },
      },
    }
  },
}
</script>
