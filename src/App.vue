<template>
  <div id="app">
    <VirtualList :fullyData="fullyData" />
  </div>
</template>

<script>
import VirtualList from './components/VirtualList.vue'

export default {
  name: 'app',
  components: {
    VirtualList
  },
  data() {
    return {
      fullyData: []
    }
  },
  created() {
    let arr = []
    const randomColor = () => {
      return Math.floor(Math.random() * 255)
    }
    for (let i = 0; i < 10000; i ++) {
      arr.push({
        value: i,
        backColor: `rgb(${randomColor()}, ${randomColor()}, ${randomColor()})`
      })
    }
    this.fullyData = arr
  }
}
</script>

<style>

</style>
