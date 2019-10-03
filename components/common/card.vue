<template>
	<view class="card">
		<!-- 标题 -->
		<view v-if="showhead" class="p-2 main-border-color" :class="getHeadClass">
			<slot name="title">
				<text v-if="headTitle" class="font-md font-weight">{{ headTitle }}</text>
			</slot>
		</view>
		<view :class="getBodyClass">
			<image v-if="bodyCover" :src="bodyCover" mode="widthFix"></image>
			<slot></slot>
		</view>
	</view>
</template>

<script>
export default {
	name: 'card',
	props: {
		// 头部标题
		headTitle: String,
		// 封面图
		bodyCover: String,
		// 是否显示头部
		showhead: {
			type: Boolean,
			default: true
		},
    headBorderBottom:{
      type: Boolean,
      default: true
    },
    bodyPadding:{
      type: Boolean,
      default: false
    }
	},
  computed: {
    getHeadClass() {
      let BorderBottom = this.headBorderBottom ? 'border-bottom':''
      return `${BorderBottom}`
    },
    getBodyClass(){
      let padding = this.bodyPadding ? 'p-2' : ''
      return `${padding}`
    }
  }
}
</script>
