<template>
	<swiper indicator-dots autoplay :interval="3000" :duration="1000" circular>
		<block :key="item.id" v-for="item of swipers">
			<swiper-item>
				<view class="swiper-item" @tap="handleclickimg(item)"><image style="height: 350upx;" :src="item.src" lazy-load></image></view>
			</swiper-item>
		</block>
	</swiper>
</template>
<script>
export default {
	name: 'swiperimage',
	props: {
		swipers: Array
	},
	methods: {
		handleclickimg(obj) {
			this.$emit('handleclickimg', obj);
		}
	}
};
</script>
