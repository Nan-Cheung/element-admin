<template>
  <div>
    <el-tooltip :content="content" placement="bottom">
      <svg-icon :icon-class="isFullscreen?'exit-fullscreen':'fullscreen'" @click="click" />
    </el-tooltip>
  </div>
</template>

<script>
  import screenfull from 'screenfull'

  export default {
    name: 'Screenfull',
    data() {
      return {
        isFullscreen: false,
        content: '全屏'
      }
    },
    mounted() {
      this.init()
    },
    beforeDestroy() {
      this.destroy()
    },
    methods: {
      click() {
        if (!screenfull.enabled) {
          this.$message({
            message: 'you browser can not work',
            type: 'warning'
          })
          return false
        }

        screenfull.toggle()
      },
      change() {
        this.isFullscreen = screenfull.isFullscreen
        this.content = screenfull.isFullscreen ? '退出全屏' : '全屏'
      },
      init() {
        if (screenfull.enabled) {
          screenfull.on('change', this.change)
        }
      },
      destroy() {
        if (screenfull.enabled) {
          screenfull.off('change', this.change)
        }
      }
    }
  }
</script>

<style scoped>
  .screenfull-svg {
    display: inline-block;
    cursor: pointer;
    fill: #5a5e66;;
    width: 20px;
    height: 20px;
    vertical-align: 10px;
  }
</style>
