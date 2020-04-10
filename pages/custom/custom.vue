<template>
	<view class="content">
		<view class="input_row">
			<view class="input_wrapper">
				<view class="uni-form-item uni-column">
					<input class="uni-input" confirm-type="search" placeholder="键盘右下角按钮显示为搜索" />
				</view>
			</view>
			<view class="btn_wrapepr"><button type="primary" size="mini">搜索</button></view>
		</view>
		<view>
			<view>
				<view></view>
				<view>
					<view></view>
					<view></view>
					<view></view>
					<view></view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.input_row{
	position: relative;
	margin-top: 10px;
	background: #fff;
}
.input_wrapper{
	width: 100%;
	box-sizing: border-box;
	padding-right: 90px;
	padding-left: 10px;
}
/* .uni-input{
	height: 29px;
} */
.btn_wrapepr{
	position: absolute;
	right: 0;
	top: 50%;
	margin-top: -14.5px;
}
</style>
