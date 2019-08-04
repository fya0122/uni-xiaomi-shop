<template>
	<view><swiper-image :swipers="swipers"></swiper-image></view>
</template>

<script>
import swiperImage from '../../components/index/swiper-image.vue';
export default {
	data() {
		return {
			swipers: [
				{
					src: '../../static/images/demo/demo4.jpg'
				},
				{
					src: '../../static/images/demo/demo4.jpg'
				},
				{
					src: '../../static/images/demo/demo4.jpg'
				}
			]
		};
	},
	components: {
		swiperImage
	}
};
</script>
