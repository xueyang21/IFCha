<template>
	<view class="IFCha_center">
		<!-- 授权头像开始 -->
		<view class="center_head">
			<image class="head_image1" :src="userInfo.avatarUrl" mode=""></image>
			<view class="head_txt">
				<view>{{ userInfo.nickName }}</view>
				<button v-show="show" type="default" open-type="getUserInfo" lang="zh_CN" @getuserinfo="getuserinfo"
				 withCredentials="true">点击授权</button>
			</view>
			<image class="head_image2" src="../../static/image/right.png" mode=""></image>
		</view>
		<!-- 授权头像结束 -->
		<!-- 宫格开始 -->
		<view class="center_money">
			<view class="money_one one_border">
				<view class="one_money">
					0.00元
				</view>
				<text>钱包</text>
			</view>
			<view class="money_one two_border">
				<view class="two_money">
					0个
				</view>
				<text>优惠</text>
			</view>
			<view class="money_one three_border">
				<view class="three_money">
					0分
				</view>
				<text>积分</text>
			</view>
		</view>
		<!-- 宫格结束 -->
		<!-- 图片开始 -->
		<image class="center_image" src="../../static/image/qq3.jpg" mode=""></image>
		<!-- 图片结束 -->
		<!-- 功能开始 -->
		<view class="center_func">
			<view class="func_address" @click="clickNavi">
				收货地址<text>></text>
			</view>
		</view>
		<!-- 功能结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userInfo: {},
				show: true
			}
		},
		onLoad() {

		},
		methods: {
			clickNavi() {
				uni.navigateTo({
					url: './address'
				})
			},
			getuserinfo(e) {
				console.log(e.detail.userInfo)
				this.userInfo = e.detail.userInfo
				if (Object.keys(this.userInfo).length === 0) {
					return this.show = true // 如果为空,返回false
				}
				return this.show = false
			}

		}
	}
</script>

<style scoped>
	.center_head {
		height: 210rpx;
		padding: 50rpx 30rpx 30rpx 30rpx;
		background-color: #000000;
	}

	.head_image1 {
		border: 1rpx solid #FFFFFF;
		width: 130rpx;
		height: 130rpx;
		border-radius: 50%;
		float: left;
		margin-right: 30rpx;
	}

	.head_txt {
		color: #FFFFFF;
		margin-top: 10rpx;
		float: left;
	}

	.head_txt view {
		font-size: 30rpx;
		margin-left: 15rpx;
	}

	.head_txt button {
		width: 150rpx;
		height: 50rpx;
		border: 3rpx solid #FFFFFF;
		border-radius: 50rpx;
		background-color: #000000;
		color: #FFFFFF;
		margin-top: 25rpx;
		margin-left: 1rpx;
		font-size: 24rpx;
		line-height: 50rpx;
	}

	.head_image2 {
		width: 35rpx;
		height: 35rpx;
		float: right;
		margin-top: 50rpx;
	}

	.center_money {
		display: flex;
		flex-wrap: wrap;
		flex: 3;
	}

	.money_one {
		width: 33.3%;
		text-align: center;
		padding: 20rpx 0;
		background-color: #FFFFFF;
	}

	.one_money {
		font-size: 36rpx;
		margin-bottom: 10rpx;
		color: #FE9900;
	}

	.two_money {
		font-size: 36rpx;
		margin-bottom: 10rpx;
		color: #FF5F3F;
	}

	.three_money {
		font-size: 36rpx;
		margin-bottom: 10rpx;
		color: #6AC20B;
	}

	.one_border {
		border-right: 1rpx solid #EEEEEE;
	}

	.two_border {
		border-left: 1rpx solid #EEEEEE;
		border-right: 1rpx solid #EEEEEE;
	}

	.three_border {
		border-left: 1rpx solid #EEEEEE;
	}

	.center_image {
		width: 100%;
		height: 400rpx;
		margin-top: 20rpx;
		margin-bottom: 20rpx;
	}

	.center_func {
		background-color: #FFFFFF;
	}

	.func_address {
		padding: 20rpx;
	}

	.func_address text {
		float: right;
		height: 30rpx;
	}
</style>
