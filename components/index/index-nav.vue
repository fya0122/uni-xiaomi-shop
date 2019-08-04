<template>
	<view class="row j-center m-2">
		<block :key="item.id" v-for="item of icons">
			<view @tap="handleclickicon(item)" class="span-4 d-flex flex-column j-center a-center py-1">
				<image style="width: 60upx;height: 60upx;" :src="item.src" mode="widthFix"></image>
				<text class="font-sm">{{ item.text }}</text>
			</view>
		</block>
	</view>
</template>

<script>
export default {
	props: {
		icons: Array
	},
	methods: {
		handleclickicon(item) {
			this.$emit('handleclickicon', item);
		}
	}
};
</script>
