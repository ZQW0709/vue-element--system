<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-25 14:22:15
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-27 10:18:38
 * @Description:
 -->
<template>
  <div class="right-item-main">
    <div class="right-main-item">
      <div class="item-background">
        <div class="item-font">
          <div class="item-font-box">
            <span style="margin:auto">111 </span>
            <img src="../../assets/上.png" class="item-font-icon">
            <!-- <div style="float:right"></div> -->
          </div>
          <div class="item-font-title">工程总数 </div>
        </div>
      </div>
      <div class="item-background">
        <div class="item-font">
          <div class="item-font-box">
            <span style="margin:auto">86 </span>
            <img src="../../assets/下.png" class="item-font-icon">
          </div>
          <div class="item-font-title">数据清洗总数 </div>
        </div>
      </div>
    </div>
    <div class="right-main-item">
      <div class="item-background">
        <div class="item-font">
          <div class="item-font-box">
            <span style="margin:auto">73 </span>

            <img src="../../assets/上.png" class="item-font-icon">
          </div>
          <div class="item-font-title">发现异常数据 </div>
        </div></div><div class="item-background">
        <div class="item-font">
          <div class="item-font-box">
            <span style="margin:auto"> 62 </span>
            <img src="../../assets/下.png" class="item-font-icon">
          </div>
          <div class="item-font-title">输出质量报告 </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import { rinseCount } from '@api/hiveCount'
import { mapGetters } from 'vuex'

export default {
  data() {
    return {
      rinseCount: {}
    }
  },
  computed: {
    ...mapGetters('time', ['MillisecondNum'])
  },
  created() {
    this.getRinseCount()
    if (this.timer) {
      clearInterval(this.timer)
    } else {
      this.timer = setInterval(() => {
        this.getRinseCount()
      }, this.MillisecondNum)
    }
  },
  destroyed() {
    clearInterval(this.timer)
  },

  methods: {
    getRinseCount() {
      // 总数统计
      rinseCount().then((res) => {
        this.rinseCount = {
          ...res.item.rinseCount
        }
      })
    }
  }
}
</script>

<style scoped>
.right-item-main {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 21vh;
}
.right-main-item {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 100%;
  height: 10vh;
  margin: auto;
}
.item-background {
  display: flex;
  flex-direction: column;
  width: 48%;
  height: 9.5vh;
  background: url('../../assets/smallrectangle1.png');
  background-repeat: repeat-x;
  background-size: 100% 100%;
}
.item-font {
  width: 50%;
  margin: auto;
  font-size: 1.5rem;
  line-height: 2.5rem;
  text-align: center;
}
.item-font-box {
  position: relative;
  display: flex;
  color: #fcf90c;
}
.item-font-icon {
  position: absolute;
  top: 35%;
  right: 0;
  width: 0.7rem;
  height: 0.9rem;
}
.item-font-title {
  font-size: 1rem;
  color: #6eb1f2;
}
</style>
