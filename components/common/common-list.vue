<template>
	<view style="width: 372.5upx;">
		<image :src="obj.cover" mode="widthFix" lazy-load></image>
		<view class="p-2 pt-1">
			<view class="font-md">{{ obj.title }}</view>
			<text class="d-block font text-light-muted">{{ obj.desc }}</text>
			<view class="d-flex my-1">
				<price>{{ obj.pprice }}</price>
				<view class="font-sm text-light-muted line-through m-1 a-self-end line-h">￥{{ obj.oprice }}</view>
			</view>
		</view>
	</view>
</template>

<script>
import price from './price.vue';
export default {
	name: 'commonlist',
	components: {
		price
	},
	props: {
		obj: Object
	}
};
</script>
