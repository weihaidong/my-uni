<template>
	<view class="content">
		<uni-swiper-dot :info="swiperInfo" :current="current" :mode="mode" :dots-styles="dotsStyles" field="content">
			<swiper class="swiper-box">
				<swiper-item v-for="(item, index) in swiperInfo" :key="index">
					<view :class="item.colorClass" class="swiper-item">
						<image class="image" :src="item.url" mode="aspectFill" />
					</view>
				</swiper-item>
			</swiper>
		</uni-swiper-dot>
		<view class="w_p">
			<view class="menu_item" v-for="(item, index) in menuData" :key="index">
				<view class="menu_header">{{item.title}}</view>
				<view class="menu_list">
					<navigator class="menu_nav"  v-for="(v, i) in item.list" :key="i" :url="v.url" hover-class="active">
						<view class="menu_img">
							<img :src="v.img">
						</view>
						<text>{{v.text}}</text>
					</navigator>
				</view>
			</view>
		</view>
		<!-- 弹出 -->
		<uni-popup ref="showtip" :type="popupType" :mask-click="false">
			<view class="uni-tip">
				<text class="uni-tip-title">未登录</text>
				<text class="uni-tip-content">您未登录，需要登录后才能继续</text>
				<view class="uni-tip-group-button">
					<text v-if="!this.forcedLogin" class="uni-tip-button" @click="cancel('tip')">取消</text>
					<text class="uni-tip-button" @click="confirm('tip')">确定</text>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import {
		mapState
	} from 'vuex'

	export default {
		computed: mapState(['forcedLogin', 'hasLogin', 'userName']),
		data(){
			return {
				menuData:[
					{
						title:'个人中心',
						list:[
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'基本资料',url:'/pages/main/main1'},
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'工资管理',url:'/pages/main/main2'},
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'招兵买马',url:'/pages/main/main3'},
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'预约购房',url:'/pages/main/main4'},
						]
					},
					{
						title:'业绩中心',
						list:[
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'个人业绩',url:'/pages/main/main5'},
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'小组业绩',url:'/pages/main/main6'},
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'团队业绩',url:'/pages/main/main7'},
						]
					},
					{
						title:'学习中心',
						list:[
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'每周答题',url:'/pages/main/main8'},
							{img:'http://thirdwx.qlogo.cn/mmopen/vi_32/7c5l6XZAuVN89nTjic4paIJOTTNJuBEnkZnBtKbiaMRNbfRAEaia7MJP7D0FiaJxEEQuAAcbPc365Z5aQgHPiaerUdw/132',text:'规章制度',url:'/pages/main/main9'},
						]
					},

				],
				swiperInfo: [{
						colorClass: 'uni-bg-red',
						url: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/shuijiao.jpg',
						content: '内容 A'
					},
					{
						colorClass: 'uni-bg-green',
						url: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/muwu.jpg',
						content: '内容 B'
					},
					{
						colorClass: 'uni-bg-blue',
						url: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/cbd.jpg',
						content: '内容 C'
					}
				],
				popupType:'',//top,bottom,center
				current: 0,//当前激活
				mode: 'dot',//default,dot,round,nav,indexes
				dotsStyles: {//圆点样式
					backgroundColor: 'rgba(0, 0, 0, .3)',
					border: '1px rgba(0, 0, 0, .3) solid',
					color: '#fff',
					selectedBackgroundColor: 'rgba(0, 0, 0, .9)',
					selectedBorder: '1px rgba(0, 0, 0, .9) solid'
				}
			}
		},
		onLoad() {
			if (!this.hasLogin) {//未登录
				// this.togglePopup('center', 'tip')
			}
		},
		methods: {
			togglePopup(type, open) {
				this.popupType = type
				this.$nextTick(() => {
					this.$refs['show' + open].open()
				})
			},
			cancel(type) {
				this.$refs['show' + type].close()
			},
			confirm(){
				if (this.forcedLogin) {
					uni.reLaunch({
						url: '../login/login'
					});
				} else {
					uni.navigateTo({
						url: '../login/login'
					});
				}
			},
		}
	}
</script>

<style>
.menu_item{
	margin-top: 10px;
}
.menu_header{
	padding: 10px;
	box-sizing: border-box;
	border: 1px solid #000;
}
.menu_list{
	margin-top: 10px;
	font-size: 0;
}
.menu_nav{
	display: inline-block;
	vertical-align: middle;
	width: calc(25% - 30px / 4);
	text-align: center;
	box-sizing: border-box;
	border: 1px solid #000;
	margin-right: 10px;
}
.menu_list .menu_nav:nth-child(4n){
	margin-right: 0;
}
.menu_img{
	width: 50px;
	height: 50px;
	border-radius: 50%;
	box-sizing: border-box;
	margin: 10px auto 0;
	border: 1px solid #000;
	overflow: hidden;
}
.menu_img img{
	width: 100%;
	height: 100%;
	object-fit: cover;
}
.menu_nav>text{
	margin-top: 10px;
	text-align: center;
	font-size: 14px;
}
</style>
