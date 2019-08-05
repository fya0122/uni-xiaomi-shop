<template>
	<view>
		<!-- 轮播图组件 -->
		<swiper-image @handleclickimg="handleclickimg" :swipers="swipers" />
		<!-- 首页分类 -->
		<index-nav @handleclickicon="handleclickicon" :icons="icons" />
		<!-- 全局分割线 -->
		<divider></divider>
		<!-- 广告 -->
		<three-adv @handleclickad="handleclickad" :threeadv="threeadv" />
		<!-- 全局分割线 -->
		<divider />
		<!-- 基础卡片 -->
		<card>
			<block slot="title">每日精选</block>
			<image src="../../static/images/bg.jpg" mode="widthFix"></image>
		</card>
	</view>
</template>

<script>
import swiperImage from '../../components/index/swiper-image.vue';
import indexNav from '../../components/index/index-nav.vue';
import divider from '../../components/common/divider.vue';
import threeAdv from '../../components/index/three-adv.vue';
import card from '../../components/common/card.vue';
export default {
	data() {
		return {
			swipers: [{ id: 1, src: '../../static/images/demo/demo4.jpg' }, { id: 2, src: '../../static/images/demo/demo4.jpg' }, { id: 3, src: '../../static/images/demo/demo4.jpg' }],
			icons: [
				{ id: 1, src: '../../static/indexnav/1.png', text: '新品发布' },
				{ id: 2, src: '../../static/indexnav/2.gif', text: '小品众筹' },
				{ id: 3, src: '../../static/indexnav/3.gif', text: '以旧换新' },
				{ id: 4, src: '../../static/indexnav/4.gif', text: '一分换图' },
				{ id: 5, src: '../../static/indexnav/5.gif', text: '超值特卖' },
				{ id: 6, src: '../../static/indexnav/6.gif', text: '小米秒卡' },
				{ id: 7, src: '../../static/indexnav/7.gif', text: '真心想要' },
				{ id: 8, src: '../../static/indexnav/8.gif', text: '电视热卖' },
				{ id: 9, src: '../../static/indexnav/9.gif', text: '家电热卖' },
				{ id: 10, src: '../../static/indexnav/10.gif', text: '米粉卡' }
			],
			threeadv: {
				big: { src: '../../static/images/demo/demo1.jpg' },
				smalltop: { src: '../../static/images/demo/demo2.jpg' },
				smallbottom: { src: '../../static/images/demo/demo2.jpg' }
			},
			bodyCover: '../../static/images/demo/demo4.jpg'
		};
	},
	components: {
		swiperImage,
		indexNav,
		threeAdv,
		divider,
		card
	},
	methods: {
		handleclickimg(obj) {
			console.log(obj);
		},
		handleclickicon(obj) {
			console.log(obj);
		},
		handleclickad(obj) {
			console.log(obj);
		}
	}
};
</script>
