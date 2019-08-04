<template>
	<swiper indicator-dots autoplay :interval="3000" :duration="1000" circular>
		<block :key="index" v-for="(item, index) of swipers">
			<swiper-item>
				<view class="swiper-item"><image style="height: 350upx;" :src="item.src" lazy-load></image></view>
			</swiper-item>
		</block>
	</swiper>
</template>
<script>
export default {
	props: {
		swipers: Array
	}
};
</script>
