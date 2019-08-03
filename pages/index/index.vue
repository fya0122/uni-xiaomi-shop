<template>
	<view>
		<view style="font-size: 50upx;" class="iconfont icon-2fanhui"></view>
		<button type="primary" @click="gotochuxian">出现吧</button>
		<view v-if="show" class="animated fadeIn fast">hello.</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			show: false
		};
	},
	onLoad() {},
	methods: {
		gotochuxian() {
			this.show = true;
		}
	}
};
</script>
