<template>
  <div 
    class="list-view"
    @scroll="handleScroll"
    >
    <div 
      class="list-view-empty"
      :style="{
        height: contentHeight
      }"
      >
    </div>
   <div
    class="list-view-content"
    
    :style="`transform: translate3d(0, ${contentTopDistance}px, 0)`"
   >
    <div 
      class="list-view-item"
      :style="{height: itemHeight + 'px', backgroundColor: item.backColor}"
      v-for="item in visibleData"
      >{{item.value}}</div>
   </div>
  </div>
</template>

<script>
export default {
  name: 'VirtualList',
  data() {
    return {
      visibleData: [],
      contentTopDistance: 0
    }
  },
  props: {
    fullyData: {
      type: Array,
      required: true
    },
    itemHeight: {
      type: Number,
      default: 60
    }
  },
  computed: {
    contentHeight() {
      return this.fullyData.length * this.itemHeight + 'px'
    }
  },
  methods: {
    updateVisibleData(scrollTop = 0) {
      // 可见区域内列表数量
      const visibleCount = Math.ceil(this.$el.clientHeight / this.itemHeight)
      // 可见区域内第一个 item 的 index
      const start = Math.floor((scrollTop / this.itemHeight))
      // 可见区域内最后一个 item 的 index
      const end = start + visibleCount + 6
      // 可见区域的 列表
      this.visibleData = this.fullyData.slice(start, end)
      this.contentTopDistance = start *  this.itemHeight
    },
    handleScroll() {
      const scrollTop = this.$el.scrollTop
      this.updateVisibleData(scrollTop)
    }
  },
  mounted() {
    this.updateVisibleData()
  }
}
</script>

<style scoped lang="scss">

.list-view {
  height: 400px;
  overflow: auto;
  position: relative;
  border: 1px solid #ddd;
  * {
    box-sizing: border-box;
  }
  .list-view-empty {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
  }
  .list-view-content {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
  }
  .list-view-item {
    color: #fff;
    line-height: 60px;
  }
}

</style>
