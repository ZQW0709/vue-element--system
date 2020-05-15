<!--
 * @LineStart: -------------------------------------------
 * @Copyright: © 2020, itclanCoder. All rights reserved.
 * @LineEnd: ----------------------------------------------
 * @Product:
 * @Mode Name:
 * @Autor: ZQW
 * @Date: 2020-03-26 17:08:25
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-03-26 17:31:04
 * @Description:
 -->
<template>
  <div class="right-item-header">
    <div class="right-item-header-right">
      <div style="margin:20px;">星期{{ week }}</div>
      <div style="margin:20px;">{{ days }}</div>
    </div>
    <div class="right-item-header-left">
      <div class="gradient-text">
        <div style="display:flex;margin:auto">
          <div style="margin:auto;"> {{ date }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weekArr: ['日', '一', '二', '三', '四', '五', '六'],
      week: '',
      days: '',
      dateForm: {
        week: '',
      },
      date: '',
    }
  },
  beforeDestroy() {
    if (this.timer) {
      clearInterval(this.timer) // 在Vue实例销毁前，清除我们的定时器
    }
  },
  created() {
    this.getTime()
  },
  methods: {
    getTime() {
      let _this = this
      this.timer = setInterval(function() {
        let times = new Date()
        let hh = times.getHours()
        let mm = times.getMinutes()
        if (mm < 10) {
          mm = '0' + mm
        }
        let ss = times.getSeconds()
        if (ss < 10) {
          ss = '0' + ss
        }
        _this.date = hh + ':' + mm + ':' + ss

        _this.week = _this.weekArr[times.getDay()]

        let yyyy = times.getFullYear()
        let MM = times.getMonth() + 1

        if (MM < 10) {
          MM = '0' + MM
        }
        let dd = times.getDate()
        if (dd < 10) {
          dd = '0' + dd
        }
        _this.days = yyyy + '-' + MM + '-' + dd
      }, 1000)
    },
  },
}
</script>

<style>
.right-item-header {
  display: flex;
  width: 100%;
  height: 9vh;
}

.right-item-header-right {
  width: 50%;
  height: 100%;
  margin-top: -20px;
  font-size: 1.5rem;
  color: #6eb1f2;
  text-align: right;
}
@media screen and (max-height: 770px) {
  .right-item-header-right {
    margin-top: -10px;
  }
}

@font-face {
  font-family: 'PingFang', sans-serif;
  font-style: normal;
  font-weight: normal;
  src: url('../font/RuiZiZhenYanTiMianFeiShangYong-2.ttf');
}
.right-item-header-left {
  display: flex;
  width: 50%;
  height: 100%;
  font-family: PingFang, sans-serif;
}
.gradient-text {
  display: flex;
  margin: auto;
  font-size: 3rem;
  line-height: 4rem;
  color: #5efcfc;
  color: transparent;
  vertical-align: bottom;
  background: linear-gradient(to bottom, #5ef9ff, #2190ff);
  -webkit-background-clip: text;
}
</style>
