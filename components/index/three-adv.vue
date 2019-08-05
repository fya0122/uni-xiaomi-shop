<template>
	<view class="d-flex">
		<image @click="handleclickad(threeadv.big)" :src="threeadv.big.src" lazy-load style="width: 373upx;height: 530upx;border-right: 2upx solid #f5f5f5;"></image>
		<view class="d-flex flex-column">
			<image @click="handleclickad(threeadv.smalltop)" :src="threeadv.smalltop.src" style="width: 375upx;height: 264upx;border-bottom: 2upx solid #f5f5f5;"></image>
			<image @click="handleclickad(threeadv.smallbottom)" :src="threeadv.smallbottom.src" style="width: 375upx;height: 264upx;"></image>
		</view>
	</view>
</template>

<script>
export default {
	name: 'threeadv',
	props: {
		threeadv: Object
	},
	methods: {
		handleclickad(item) {
			this.$emit('handleclickad', item);
		}
	}
};
</script>
