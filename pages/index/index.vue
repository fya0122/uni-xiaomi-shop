<template>
	<view class="uni-tab-bar">
		<!-- 顶部导航 -->
		<scroll-view id="tab-bar" class="uni-swiper-tab" scroll-x :scroll-left="scrollLeft">
			<view
				v-for="(tab, index) in tabBars"
				:key="tab.id"
				class="swiper-tab-list"
				:class="tabIndex == index ? 'active' : ''"
				:id="tab.id"
				:data-current="index"
				@click="tapTab(index)"
			>
				<view class="tabitems">{{ tab.name }}</view>
			</view>
		</scroll-view>
		<!-- 根据顶部变化的下面 -->
		<swiper :current="tabIndex" class="swiper-box" :duration="300" @change="changeTab">
			<swiper-item v-for="(tab, index1) in newsitems" :key="index1">
				<scroll-view class="list" scroll-y @scrolltolower="loadMore(index1)">
					<!-- index的模板 -->
					<template v-if="tabBars[index1].template === 'index'">
						<block v-for="(v, i) in tab.data" :key="i">
							<template v-if="v.type === 'swiper'">
								<!-- 轮播图组件 -->
								<swiper-image @handleclickimg="handleclickimg" :swipers="v.data" />
							</template>
							<template v-else-if="v.type === 'indexnavs'">
								<!-- 首页分类 -->
								<index-nav @handleclickicon="handleclickicon" :icons="v.data" />
								<!-- 全局分割线 -->
								<divider></divider>
							</template>
							<template v-else-if="v.type === 'threeAdv'">
								<!-- 广告 -->
								<three-adv @handleclickad="handleclickad" :threeadv="v.data" />
								<!-- 全局分割线 -->
								<divider />
							</template>
							<template v-else-if="v.type === 'oneAdv'">
								<!-- 基础卡片 -->
								<card>
									<block slot="title">{{ v.data.title }}</block>
									<image :src="v.data.cover" mode="widthFix"></image>
								</card>
							</template>
							<template v-else-if="v.type === 'list'">
								<!-- 公共列表组件 -->
								<view class="row j-sb">
									<block v-for="(vlist, index) of v.data" :key="index"><common-list :obj="vlist"></common-list></block>
								</view>
							</template>
						</block>
					</template>
					<!-- special的模板 -->
					<template v-if="tabBars[index1].template === 'special'">
						<block v-for="(v, i) in tab.data" :key="i">
							<template v-if="v.type === 'swiper'">
								<!-- 轮播图组件 -->
								<swiper-image @handleclickimg="handleclickimg" :swipers="v.data" />
							</template>
							<template v-else-if="v.type === 'indexnavs'">
								<!-- 首页分类 -->
								<index-nav @handleclickicon="handleclickicon" :icons="v.data" />
								<!-- 全局分割线 -->
								<divider></divider>
							</template>
							<template v-else-if="v.type === 'list'">
								<card headTitle="热卖爆品">
									<!-- 公共列表组件 -->
									<view class="row j-sb">
										<block v-for="(vlist, index) of v.data" :key="index"><common-list :obj="vlist"></common-list></block>
									</view>
								</card>
							</template>
						</block>
					</template>

					<!-- 加载更多 -->
					<view class="uni-tab-bar-loading">{{ tab.loadingText }}</view>
				</scroll-view>
			</swiper-item>
		</swiper>
	</view>
</template>
<script>
import swiperImage from '../../components/index/swiper-image.vue';
import indexNav from '../../components/index/index-nav.vue';
import divider from '../../components/common/divider.vue';
import threeAdv from '../../components/index/three-adv.vue';
import card from '../../components/common/card.vue';
import commonList from '../../components/common/common-list.vue';
export default {
	components: {
		swiperImage,
		indexNav,
		threeAdv,
		divider,
		card,
		commonList
	},
	data() {
		return {
			scrollLeft: 0,
			isClickChange: false,
			tabIndex: 0,
			newsitems: [
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] },
				{ loadingText: '加载更多...', data: [] }
			],
			tabBars: [
				{ name: '关注', id: 'guanzhu', template: 'index' },
				{ name: '推荐', id: 'tuijian', template: 'special' },
				{ name: '体育', id: 'tiyu', template: 'special' },
				{ name: '热点', id: 'redian', template: 'special' },
				{ name: '财经', id: 'caijing', template: 'special' },
				{ name: '娱乐', id: 'yule', template: 'special' },
				{ name: '军事', id: 'junshi', template: 'special' },
				{ name: '历史', id: 'lishi', template: 'special' },
				{ name: '本地', id: 'bendi', template: 'special' }
			]
		};
	},
	onLoad() {
		this.newsitems = this.randomfn();
	},
	methods: {
		// 加载更多
		loadMore(e) {
			setTimeout(() => {
				this.addData(e);
			}, 1200);
		},
		// 加载更多模拟数据
		addData(e) {
			if (this.newsitems[e].data.length > 30) {
				this.newsitems[e].loadingText = '没有更多了';
				return;
			}
			// this.newsitems[e].data.push(tpl['data' + Math.floor(Math.random() * 5)]);
			let arr = [
				// 轮播图
				{
					type: 'swiper',
					data: [{ id: 1, src: '../../static/images/demo/demo4.jpg' }, { id: 2, src: '../../static/images/demo/demo4.jpg' }, { id: 3, src: '../../static/images/demo/demo4.jpg' }]
				},
				// icons
				{
					type: 'indexnavs',
					data: [
						{ id: 1, src: '../../static/indexnav/1.png', text: '新品发布' },
						{ id: 2, src: '../../static/indexnav/2.gif', text: '小品众筹' },
						{ id: 3, src: '../../static/indexnav/3.gif', text: '以旧换新' },
						{ id: 4, src: '../../static/indexnav/4.gif', text: '一分换图' },
						{ id: 5, src: '../../static/indexnav/5.gif', text: '超值特卖' }
					]
				},
				// 列表
				{
					type: 'list',
					data: [
						{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调1', desc: '1.5匹变频', oprice: 2699, pprice: 1399, id: 1 },
						{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调2', desc: '1.5匹变频', oprice: 2698, pprice: 1398, id: 2 },
						{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调3', desc: '1.6匹变频', oprice: 2697, pprice: 1397, id: 3 },
						{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调4', desc: '1.7匹变频', oprice: 2696, pprice: 1396, id: 4 },
						{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调4', desc: '1.9匹变频', oprice: 2695, pprice: 1395, id: 5 }
					]
				}
			];

			this.newsitems[e].data = [...this.newsitems[e].data, ...arr]; // 算是合并吧
			console.log(this.newsitems[e].data);
		},
		// 异步的改变tab
		async changeTab(e) {
			let index = e.target.current;
			if (this.newsitems[index].data.length === 0) {
				this.addData(index);
			}
			if (this.isClickChange) {
				this.tabIndex = index;
				this.isClickChange = false;
				return;
			}
			let tabBar = await this.getElSize('tab-bar'),
				tabBarScrollLeft = tabBar.scrollLeft;
			let width = 0;

			for (let i = 0; i < index; i++) {
				let result = await this.getElSize(this.tabBars[i].id);
				width += result.width;
			}
			let winWidth = uni.getSystemInfoSync().windowWidth,
				nowElement = await this.getElSize(this.tabBars[index].id),
				nowWidth = nowElement.width;
			if (width + nowWidth - tabBarScrollLeft > winWidth) {
				this.scrollLeft = width + nowWidth - winWidth;
			}
			if (width < tabBarScrollLeft) {
				this.scrollLeft = width;
			}
			this.isClickChange = false;
			this.tabIndex = index; //一旦访问data就会出问题
		},
		getElSize(id) {
			//得到元素的size
			return new Promise((res, rej) => {
				uni
					.createSelectorQuery()
					.select('#' + id)
					.fields(
						{
							size: true,
							scrollOffset: true
						},
						data => {
							res(data);
						}
					)
					.exec();
			});
		},
		// 点击tabbar的
		async tapTab(e) {
			//点击tab-bar
			// let tabIndex = e.target.dataset.current;
			// new，点击的索引
			let tabIndex = e;
			if (this.newsitems[tabIndex].data.length === 0) {
				this.addData(tabIndex);
			}
			if (this.tabIndex === tabIndex) {
				return false;
			} else {
				let tabBar = await this.getElSize('tab-bar'),
					tabBarScrollLeft = tabBar.scrollLeft; //点击的时候记录并设置scrollLeft
				this.scrollLeft = tabBarScrollLeft;
				this.isClickChange = true;
				this.tabIndex = tabIndex;
			}
		},
		// 生成随机数据
		randomfn() {
			let ary = [];
			const tabBarsLength = this.tabBars.length;
			for (let i = 0; i < tabBarsLength; i++) {
				let aryItem = {
					loadingText: '加载更多...',
					data: []
				};
				if (this.tabBars[i].template === 'index') {
					aryItem.data = [
						// 轮播图
						{
							type: 'swiper',
							data: [
								{ id: 1, src: '../../static/images/demo/demo4.jpg' },
								{ id: 2, src: '../../static/images/demo/demo4.jpg' },
								{ id: 3, src: '../../static/images/demo/demo4.jpg' }
							]
						},
						// icons
						{
							type: 'indexnavs',
							data: [
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
							]
						},
						// 三个图的广告
						{
							type: 'threeAdv',
							data: {
								big: { src: '../../static/images/demo/demo1.jpg' },
								smalltop: { src: '../../static/images/demo/demo2.jpg' },
								smallbottom: { src: '../../static/images/demo/demo2.jpg' }
							}
						},
						// 大图广告
						{
							type: 'oneAdv',
							data: {
								title: '每日精选',
								cover: '../../static/images/demo/demo4.jpg'
							}
						},
						// 列表
						{
							type: 'list',
							data: [
								{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调1', desc: '1.5匹变频', oprice: 2699, pprice: 1399, id: 1 },
								{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调2', desc: '1.5匹变频', oprice: 2698, pprice: 1398, id: 2 },
								{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调3', desc: '1.6匹变频', oprice: 2697, pprice: 1397, id: 3 },
								{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调4', desc: '1.7匹变频', oprice: 2696, pprice: 1396, id: 4 },
								{ cover: '../../static/images/demo/list/1.jpg', title: '米家空调4', desc: '1.9匹变频', oprice: 2695, pprice: 1395, id: 5 }
							]
						}
					];
				}
				ary.push(aryItem);
			}
			return ary;
		}
	}
};
</script>

<style scoped>
.tabitems {
	display: inline-block;
	width: 75upx;
	border-bottom: 5upx solid #fff;
}
.active .tabitems {
	border-bottom: 5upx solid #fd6801;
}
.uni-tab-bar-loading {
	text-align: center;
	font-size: 28upx;
	color: #999;
}
</style>
