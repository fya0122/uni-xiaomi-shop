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
      <view class="flex-1 d-flex a-center j-center main-text-color" @click="showRigth = true">筛选</view>
    </view>
    <!-- 右侧滑出的抽屉 -->
    <uni-drawer :visible="showRigth" mode="right" @close="showRigth = false">
      <card headTitle="服务" :headBorderBottom="false" :headTitleWeight="false">
        <view>111</view>
      </card>
      <!-- 按钮 -->
      <view class="d-flex position-fixed bottom-0 right-0 w-100 border-top border-light-secondary">
        <view class="flex-1 main-bg-color text-white font-md py-2 text-center" hover-class="main-bg-hover-color">确定</view>
        <view class="flex-1 font-md py-2 text-center" hover-class="bg-light-secondary">重置</view>
      </view>
    </uni-drawer>
  </view>
</template>
<script>
import uniDrawer from "@/components/uni-ui/uni-drawer/uni-drawer.vue"
import card from "@/components/common/card.vue"
export default {
  components: {
    uniDrawer,
    card
  },
  data() {
    return {
      showRigth: false,
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