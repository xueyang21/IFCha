<template>
	<view class="IFCha_address">
		<view v-show="show" class="address_head">
			<view class="head_box">
				<view class="box1">
					收货人：{{ address.name }}<text>{{address.tel}}</text>
				</view>
				<view class="box2">
					收货地址： {{address.value!='' ? address.value : add}}
				</view>
			</view>
		</view>
		<view class="address_box">
			<view class="address_btn">
				<view class="btn btn1">
					<button class="" type="default" @click="clickNavi">手动添加</button>
				</view>
				<view class="btn btn2">
					<button class="" type="default" @click="clickNavi2">微信添加</button>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				address:{},
				show:false,
				add:''
			}
		},
		onLoad(option) {
			console.log(option)
			this.address = option
			this.add = option.addAdd + option.addName
			if (Object.keys(option).length === 0) {
			    return this.show = false // 如果为空,返回false
			}
			return this.show = true
		},
		methods: {
			clickNavi(){
				uni.navigateTo({
					url:'./edit'
				})
			},
			clickNavi2(){
				uni.navigateTo({
					url:'./shipping'
				})
			}
		}
	}
</script>

<style>
	.address_head{
		padding: 30rpx;
		border-bottom:1rpx solid #E5E5E5;
	}
	.box1{
		margin-bottom: 30rpx;
	}
	.box1 text{
		float: right;
		margin-right: 20rpx;
	}
	
	.address_box{
		width: 100%;
		position: fixed;
		bottom: 10rpx;
	}
	.address_btn{
		display: flex;
		flex-wrap: wrap;
		flex: 1;
	}
	
	.btn{
		width: 45%;
		margin-left: 3.3%;
	}
	.btn1 button{
		background-color: #000000;
		color: #FFFFFF;
	}
	.btn2 button{
		background-color: #09BA07;
		color: #FFFFFF;
	}
</style>
