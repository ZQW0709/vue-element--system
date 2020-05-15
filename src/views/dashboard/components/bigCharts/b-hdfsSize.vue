<template>
  <div class="item-first-main-size">
    <div
      v-for="(item, index) of hdfsSizeList"
      :key="index"
      style="display:flex;"
      :style="{
        width: item !== '.' ? '19%' : '1%',
      }"
    >
      <div v-if="item !== '.'" class="item-title-font">
        <span class="num-class">{{ item }}</span>
      </div>
      <div v-else class="point-class">
        <span>.</span>
      </div>
    </div>
  </div>
</template>

<script>
// import { hdfsSize } from '@api/hiveCount'
import { mapGetters } from 'vuex'
export default {
  data() {
    return {
      hdfsSize: '',
      hdfsSizeList: []
    }
  },
  computed: {
    ...mapGetters('time', ['MillisecondNum'])
  },
  mounted() {
    this.getHdfsSize()
    if (this.timer) {
      clearInterval(this.timer)
    } else {
      this.timer = setInterval(() => {
        this.getHdfsSize()
      }, this.MillisecondNum)
    }
  },
  destroyed() {
    clearInterval(this.timer)
  },
  methods: {
    async getHdfsSize() {
      const res = await hdfsSize()
      this.hdfsSize = res.item.hdfsSize.GB
      this.hdfsSizeList = []
      const tempList = this.hdfsSize.toString()
      for (let i = 0; i < tempList.length; i++) {
        this.hdfsSizeList.push(tempList[i])
      }
    }
  }
}
</script>

<style scoped>
.item-first-main-size {
  position: absolute;
  top: 28%;
  left: 34%;
  display: flex;
  justify-content: flex-start;
  width: 40%;
  height: 10%;
  font-size: 3.875rem;
  color: #0ff;
}
.item-title-font {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  margin-left: 20px;
  font-size: 3.875rem;
  color: #0ae8f8;

  /* background: aquamarine; */
  background-image: linear-gradient(
    rgb(93, 136, 252) 50%,
    rgb(36, 89, 221) 51%
  );
  border-radius: 5px;
}
.num-class {
  /* margin: auto; */
  margin-top: -0.5rem;
}

.point-class {
  position: relative;
  top: -15%;
  left: 120%;

  /* bottom: 24%; */

  /* left: 19%; */
}
</style>
