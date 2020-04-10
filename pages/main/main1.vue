<template>
    <view class="content">
        <view class="w_p">
			<view class="uni-form-item uni-column">
				<view class="title">工号</view>
				<input class="uni-input" name="input" :disabled="true" placeholder="工号" v-model="datas.gh" />
			</view>
			<view class="uni-form-item uni-column">
				<view class="title">小组</view>
				<input class="uni-input" name="input" :disabled="true" placeholder="小组" v-model="datas.xz" />
			</view>
			<view class="uni-form-item uni-column">
				<view class="title">姓名</view>
				<input class="uni-input" name="input" placeholder="姓名" v-model="datas.name" />
			</view>
			<view class="uni-form-item uni-column">
				<view class="title">性别</view>
				<radio-group name="radio">
					<label>
						<radio value="1" :checked="datas.sex==1"/><text>选项一</text>
					</label>
					<label>
						<radio value="2" :checked="datas.sex==2"/><text>选项二</text>
					</label>
				</radio-group>
			</view>
			<view class="uni-form-item uni-column">
				<view class="title">联系电话</view>
				<input class="uni-input" name="input" placeholder="联系电话" v-model="datas.phone" />
			</view>
			<view class="uni-form-item uni-column">
				<view class="title">身份证号</view>
				<input class="uni-input" name="input" placeholder="身份证号" v-model="datas.c_id" />
			</view>
			<view class="uni-form-item uni-column">
				<view class="title">本人银行卡号(工商银行)</view>
				<input class="uni-input" name="input" placeholder="本人银行卡号(工商银行)" v-model="datas.b_num" />
			</view>
			<view class="uni-form-item uni-column">
				<view class="title">推介人</view>
				<input class="uni-input" name="input" :disabled="true" placeholder="推介人" v-model="datas.tjr" />
			</view>
			<view class="uni-btn-v">
				<button @click="formSubmit('btn1')" :disabled="btns['btn1']" :loading="loading['btn1']">Submit</button>
			</view>
        </view>
    </view>
</template>
<script>
    export default {
        data() {
            return {
				datas:{
					gh:'054219',
					xz:'成都YF组',
					name:'asd',
					sex:'1',
					phone:'',
					c_id:'',
					b_num:'',
					tjr:'成都YF组-章友福-054218',
				},
				btns:{
					btn1:false
				},
				loading:{
					btn1:false
				}
            }
		},
		onLoad: function(){
		},
        methods: {
            formSubmit: function(btn) {
				var _this=this
				if(!_this.btns[btn]){
					_this.btns[btn]=true
					_this.loading[btn]=true
					uni.request({
						url: 'https://www.example.com/request', //仅为示例，并非真实接口地址。
						data: _this.datas,
						header: {
							'custom-header': 'hello' //自定义请求头信息
						},
						method:'POST',
						timeout:'20000',
						success: (res) => {
							_this.btns[btn]=false
							_this.loading[btn]=false

							uni.switchTab({
								url: '/pages/main/main'
							});
						},
						fail:(res)=>{
							_this.btns[btn]=false
							_this.loading[btn]=false
							uni.switchTab({
								url: '/pages/main/main'
							});
						}
					});
				}
            }
        }
    }
</script>

<style>
    
</style>