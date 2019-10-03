<template>
  <view>
    <!-- 排序筛选 -->
    <view class="d-flex botder-top border-bottom a-center j-center" style="height: 100upx;">
      <view @click="changeScreen(index)" :key="item.name" v-for="(item, index) of screen.list" class="flex-1 d-flex a-center j-center font-md">
        <text :class="screen.currentIndex === index ? 'main-text-color' : 'text-muted'">{{ item.name }}</text>
        <view>
          <view :class="item.status === 1 ? 'main-text-color' : 'text-light-muted'" class="iconfont icon-paixu-shengxu line-h0"></view>
          <view :class="item.status === 2 ? 'main-text-color' : 'text-light-muted'" class="iconfont icon-paixu-jiangxu line-h0"></view>
        </view>
      </view>
      <view class="flex-1 d-flex a-center j-center main-text-color">筛选</view>
    </view>
  </view>
</template>
<script>
export default {
  data() {
    return {
      screen: {
        currentIndex: 0,
        list: [
          { name: '综合', status: 1 },
          { name: '销量', status: 0 },
          { name: '价格', status: 0 },
        ]
      }
    }
  },
  methods: {
    changeScreen(index) {
      // if (this.screen.currentIndex === index) {
      //   if (this.screen.list[index].status === 1) {
      //     this.screen.list[index].status = 2
      //   } else {
      //     this.screen.list[index].status = 1
      //   }
      // } else {
      //   this.screen.currentIndex = index
      //   for (const item of this.screen.list) {
      //     item.status = 0
      //   }
      //   this.screen.list[index].status = 2
      // }
      
      // 旧的当前的index
      let oldIndex = this.screen.currentIndex
      let oldItem = this.screen.list[oldIndex]
      // 如果旧的当前的index跟你点击的那个index是一样，我们只需要改变状态即可
      if (oldIndex === index) {
        // 赋值
        return oldItem.status = oldItem.status === 1 ? 2 : 1
      }
      
      // 否则我们处理新的逻辑
      let newItem = this.screen.list[index]
      oldItem.status = 0
      this.screen.currentIndex = index
      newItem.status = 1
    }
  }
}
</script>
<style></style>