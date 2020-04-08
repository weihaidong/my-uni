<template>
	<view class="content">
		<uni-swiper-dot :info="info" :current="current" :mode="mode" :dots-styles="dotsStyles" field="content">
			<swiper class="swiper-box" @change="changeBox">
				<swiper-item v-for="(item, index) in info" :key="index">
					<view :class="item.colorClass" class="swiper-item">
						<image class="image" :src="item.url" mode="aspectFill" />
					</view>
				</swiper-item>
			</swiper>
		</uni-swiper-dot>
		<uni-section title="模式选择" type="line"></uni-section>
		<view class="example-body">
			<view :class="{ active: modeIndex === 0 }" class="example-body-item" @click="selectMode('default', 0)"><text class="example-body-item-text">default</text></view>
			<view :class="{ active: modeIndex === 1 }" class="example-body-item" @click="selectMode('dot', 1)"><text class="example-body-item-text">dot</text></view>
			<view :class="{ active: modeIndex === 2 }" class="example-body-item" @click="selectMode('round', 2)"><text class="example-body-item-text">round</text></view>
			<view :class="{ active: modeIndex === 3 }" class="example-body-item" @click="selectMode('nav', 3)"><text class="example-body-item-text">nav</text></view>
			<view :class="{ active: modeIndex === 4 }" class="example-body-item" @click="selectMode('indexes', 4)"><text class="example-body-item-text">indexes</text></view>
		</view>
		<uni-section title="颜色样式选择" type="line"></uni-section>
		<view class="example-body">
			<template v-if="mode !== 'nav'">
				<view v-for="(item, index) in dotStyle" :class="{ active: styleIndex === index }" :key="index" class="example-body-item"
				 @click="selectStyle(index)">
					<view :style="{ 'background-color': item.selectedBackgroundColor, border: item.selectedBorder }" class="example-body-dots" />
					<view :style="{ 'background-color': item.backgroundColor, border: item.border }" class="example-body-dots" />
					<view :style="{ 'background-color': item.backgroundColor, border: item.border }" class="example-body-dots" />
				</view>
			</template>
			<template v-if="mode === 'nav'">
				<view v-for="(item, index) in dotStyle" :class="{ active: styleIndex === index }" :key="index" :style="{ 'background-color': item.selectedBackgroundColor }"
				 class="example-body-item" @click="selectStyle(index)">
					<text class="example-body-item-text" :style="{ color: item.color }">内容</text>
				</view>
			</template>
		</view>


		<view v-if="hasLogin" class="hello">
			<view class="title">
				您好 {{userName}}，您已成功登录。
			</view>
			<view class="ul">
				<view>这是 uni-app 带登录模板的示例App首页。</view>
				<view>在 “我的” 中点击 “退出” 可以 “注销当前账户”</view>
			</view>
		</view>
		<view v-if="!hasLogin" class="hello">
			<view class="title">
				您好 游客。
			</view>
			<view class="ul">
				<view>这是 uni-app 带登录模板的示例App首页。</view>
				<view>在 “我的” 中点击 “登录” 可以 “登录您的账户”</view>
			</view>
		</view>

		<!-- 弹出 -->
		<uni-popup ref="showtip" :type="type" :mask-click="false" @change="change">
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
				info: [{
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
				dotStyle: [{
						backgroundColor: 'rgba(0, 0, 0, .3)',
						border: '1px rgba(0, 0, 0, .3) solid',
						color: '#fff',
						selectedBackgroundColor: 'rgba(0, 0, 0, .9)',
						selectedBorder: '1px rgba(0, 0, 0, .9) solid'
					},
					{
						backgroundColor: 'rgba(255, 90, 95,0.3)',
						border: '1px rgba(255, 90, 95,0.3) solid',
						color: '#fff',
						selectedBackgroundColor: 'rgba(255, 90, 95,0.9)',
						selectedBorder: '1px rgba(255, 90, 95,0.9) solid'
					},
					{
						backgroundColor: 'rgba(83, 200, 249,0.3)',
						border: '1px rgba(83, 200, 249,0.3) solid',
						color: '#fff',
						selectedBackgroundColor: 'rgba(83, 200, 249,0.9)',
						selectedBorder: '1px rgba(83, 200, 249,0.9) solid'
					}
				],
				modeIndex: -1,
				styleIndex: -1,
				current: 0,
				mode: 'default',
				dotsStyles: {}
			}
		},
		onLoad() {
			if (!this.hasLogin) {
				this.togglePopup('center', 'tip')
			}
		},
		methods: {
			togglePopup(type, open) {
				switch (type) {
					case 'top':
						this.content = '顶部弹出 popup'
						break

					case 'bottom':
						this.content = '底部弹出 popup'
						break
					case 'center':
						this.content = '居中弹出 popup'
						break
				}
				this.type = type
				this.$nextTick(() => {
					this.$refs['show' + open].open()
				})
			},
			cancel(type) {
				this.$refs['show' + type].close()
			},
			changeBox(e) {
				console.log('是否打开:' + e.show)
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
			change(e) {
				uni.showToast({
					icon: 'none',
					title: '已发送重置邮件至注册邮箱，请注意查收。',
					duration: 100
				});
				// this.current = e.detail.current
			},
			selectStyle(index) {
				this.dotsStyles = this.dotStyle[index]
				this.styleIndex = index
			},
			selectMode(mode, index) {
				this.mode = mode
				this.modeIndex = index
				this.styleIndex = -1
				this.dotsStyles = this.dotStyle[0]
			}
		}
	}
</script>

<style>
	.hello {
		display: flex;
		flex: 1;
		flex-direction: column;
	}

	.title {
		color: #8f8f94;
		margin-top: 25px;
	}

	.ul {
		font-size: 15px;
		color: #8f8f94;
		margin-top: 25px;
	}

	.ul>view {
		line-height: 25px;
	}
</style>
