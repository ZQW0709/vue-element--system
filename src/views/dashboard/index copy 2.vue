<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-23 17:28:41
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-27 10:58:15
 * @Description:大屏图
 -->
<template>
  <div class="container">
    <div class="b-left">
      <div class="b-left-item">
        <div class="item-title">
          <div style="margin-top: 1%; margin-left: 2%;">近七日工程运行数量</div>
        </div>
        <bHistogram />
      </div>
      <div class="b-left-item">
        <div class="item-title">
          <div style="margin-top: 1%; margin-left: 2%;">近24小时整体趋势</div>
        </div>
        <b-line />
      </div>
      <div class="b-left-item">
        <div class="item-title">
          <div style="margin-top: 1%; margin-left: 2%;">API网关情况</div>
        </div>
        <bPie />
      </div>
    </div>
    <div class="b-center">
      <div class="b-center-item b-center-item-first">
        <div class="item-first-header">
          <!-- <div>LDH&LW数据监控驾驶舱</div> -->
          <div class="gradient-text">
            <div style="display:flex;height:3rem;margin:auto">
              <div class="gradient-text-title"> LDH&LW数据监控驾驶舱</div>
            </div>
          </div>
        </div>
        <div
          class="item-first-main"
        ><bMap />
          <b-hdfsSize />
          <div class="item-first-main-pie">
            <div class="line-header">
              <div>数仓情况</div>
            </div>
            <bPiethree />
          </div>
        </div>
      </div>
      <div class="b-center-item b-center-item-second">
        <div style="width:50%;height:31vh">
          <div class="second-container">
            <div class="b-center-item-second-header">
              <div class="line-header">
                <div>算子分类(占比)</div>
              </div>
            </div>
            <div class="container-item">
              <div class="second-container-item">
                <div class="second-container-item-title">
                  <div>算子种类</div>
                  <div style="font-size:2rem;color: #FFF">{{
                    figureForm.算子种类
                  }}</div>
                </div>
              </div>
              <div class="second-container-item">
                <div class="second-container-item-title">
                  <div>算子个数</div>
                  <div style="font-size:2rem;color: #FFF">{{
                    figureForm.算子个数
                  }}</div>
                </div>
              </div>
            </div>
          </div>
          <div class="second-container"> <bPietwo /> </div>
        </div>
        <div style="width:50%;height:31vh;">
          <div class="b-center-item-second-header">
            <div class="line-header">
              <div>数据源类型</div>
            </div>
          </div>
          <div style="display:flex;width:100%;height:27.5vh">
            <bRadar />
          </div>
        </div>
      </div>
    </div>
    <div class="b-right">
      <div class="b-right-item">
        <bTimes />

        <b-info style="margin-top:5px" />
      </div>
      <div class="b-left-item">
        <div class="item-title">
          <div
            style="margin-top: 1%; margin-left: 2%;"
          >近七日数据处理量(W)</div>
        </div>
        <b-linetwo />
      </div>
      <div class="b-left-item">
        <div class="item-title">
          <div style="margin-top: 1%; margin-left: 2%;">数据异常类型(个)</div>
        </div>
        <b-bar />
      </div>
    </div>
  </div>
</template>

<script>
import bHistogram from './components/bigCharts/b-histogram'
import bLine from './components/bigCharts/b-line'
import bLinetwo from './components/bigCharts/b-linetwo'
import bPie from './components/bigCharts/b-pie'
import bPietwo from './components/bigCharts/b-pietwo'
import bPiethree from './components/bigCharts/b-piethree'
import bInfo from './components/bigCharts/b-info'
import bBar from './components/bigCharts/b-bar'
import bRadar from './components/bigCharts/b-radar'
import bMap from './components/bigCharts/b-map'
import bTimes from './components/bigCharts/b-times'
import bHdfsSize from './components/bigCharts/b-hdfsSize'
// import { figureNumCount } from '@api/hiveCount'
export default {
  components: {
    bHistogram,
    bLine,
    bPie,
    bPietwo,
    bPiethree,
    bLinetwo,
    bInfo,
    bBar,
    bRadar,
    bMap,
    bTimes,
    bHdfsSize
  },
  data() {
    return {
      date: '',
      figureForm: {}
    }
  },
  created() {
    this.getFigureNumCount()
  },
  methods: {
    getFigureNumCount() {
      // 算子种类和个数
      figureNumCount().then((res) => {
        this.figureForm = {
          ...res.item.figureNumCount
        }
      })
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  width: 100vw;
  height: 100vh;
  background: url('./assets/bg1.png');
  background-repeat: repeat-x;
  background-size: 100% 100%;
}

.b-left {
  display: flex;
  flex-direction: column;
  width: 25%;
  height: 100vh;
}

.b-right-item {
  flex-direction: column;
  width: 100%;
  height: 31vh;
  margin: auto;
}

.b-left-item {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 31vh;
  margin: auto;
  background: url('./assets/rectangle.png');
  background-repeat: repeat-x;
  background-size: 100% 100%;
}

.item-title {
  display: flex;
  width: 50%;
  height: 3.5vh;
  padding: 5px;
  font-size: 1.125rem;
  color: #5efcfc;
}

.left-three {
  width: 98%;
  height: 31vh;
  margin: auto;
  background-color: rgb(70, 16, 219);
}

.b-center {
  display: flex;
  flex-direction: column;
  width: 48%;
  height: 100vh;
}
.b-center-item {
  display: flex;
  width: 100%;
  margin: auto;
}
.b-center-item-first {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 64vh;
}
.item-first-header {
  display: flex;
  width: 80%;
  height: 9vh;
  background: url('./assets/center.png');
  background-repeat: repeat-x;
  background-size: 100% 100%;
}
.gradient-text-title {
  margin: auto;
  font-size: 2.5rem;
  line-height: 3rem;
  color: transparent;
  vertical-align: bottom;
  background: linear-gradient(to bottom, #5ef9ff, #2190ff);
  -webkit-background-clip: text;
}
.item-first-main {
  width: 100%;
  height: 52vh;
}

/* .item-first-main-size {
  position: absolute;
  top: 28%;
  left: 40%;
  font-size: 2rem;
  font-size: 3.875rem;
  color: #0ff;
} */
.item-first-main-pie {
  position: absolute;
  bottom: 1.2vw;
  width: 10vw;
  height: 10vw;
}
.b-center-item-second {
  height: 31vh;
}
.second-container {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 50%;
}
.container-item {
  display: flex;
  width: 100%;
  height: 14vh;
}
.second-container-item {
  display: flex;
  width: 35%;
  height: 80%;
  margin: auto;
  background: url('./assets/Hexagon.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;

  /* background-repeat: repeat-x; */

  /* background-size: 100% 100%; */
}
.second-container-item-title {
  margin: auto;
  line-height: 2.2rem;
  color: #6eb1f2;
  text-align: center;
}
.b-center-item-second-header {
  width: 100%;
  height: 3.6vh;
}
.line-header {
  display: flex;
  align-content: center;
  align-items: center;
  font-size: 1.125rem;
  color: #0ff;
}
.line-header::before {
  display: inline;
  width: 10px;
  height: 2vh;
  margin-right: 10px;
  content: '';
  background-color: #0ff;
}

.b-right {
  display: flex;
  flex-direction: column;
  width: 25vw;
  height: 100vh;
}
</style>
