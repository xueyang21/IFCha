<template>
	<view class="IFCha_member">
		<!-- 轮播开始 -->
		<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
			<swiper-item v-for="banner in banners" :key="index">
				<image class="banner" :src="banner.photo" mode=""></image>
			</swiper-item>
		</swiper>
		<!-- 轮播结束 -->
		<!-- 会员特权开始 -->
		<view class="member_title">
			会员特权
			<view class="title_txt">
				<image src="../../static/image/wenhao.png" />
				<text>特权说明</text>
			</view>
			<view class="title_image">
				<image src="../../static/image/image.png" mode=""></image>
			</view>
		</view>
		<!-- 会员特权结束 -->
		<!-- 专属优惠开始 -->
		<view class="member_content">
			<view class="content_title">
				买单享受专属折扣
			</view>
			<view class="content_title2">
				会员期内买单可享受
				<text>折扣优惠</text>
			</view>
			<view class="content_image">
				<image src="../../static/image/image2.png" mode=""></image>
			</view>
		</view>
		<view class="member_txt">
			IFCha一夫茶会员是IFCha一夫茶小程序为用户提供的一项增值服务，包含多项会员专属权益，更多权益策略还在不断完善中，敬请期待。会员卡一经办理，不支持退款。会员红包不支持现金兑换，仅可用于购买商品和抵扣使用。
		</view>
		<!-- 专属优惠结束 -->
		<!-- 开通会员按钮开始 -->
		<view class="member_btn">
			<button type="default">开通会员>></button>
		</view>
		<!-- 开通会员按钮结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				banners: [{
					photo: require('../../static/image/qq3.jpg')
				}],
			}
		}
	}
</script>

<style scoped>
	.IFCha_member {
		background-color: #F4F4F4;
	}

	.swiper {
		width: 100%;
	}

	.banner {
		width: 100%;
		height: 300rpx;
	}

	.member_title {
		background-color: #FFFFFF;
		font-size: 35rpx;
		font-weight: 600;
		color: #555555;
		text-align: center;
		height: 280rpx;
		padding-top: 20rpx;
	}

	.member_title image {
		width: 40rpx;
		height: 40rpx;
	}

	.title_txt {
		font-size: 30rpx;
		font-weight: 400;
		color: #999999;
	}

	.title_txt text {
		float: right;
		margin-top: -40rpx;
		margin-right: 65rpx;
	}

	.title_txt image {
		float: right;
		margin-top: -40rpx;
		margin-right: 20rpx;
	}

	.title_image {
		margin-top: 20rpx;
	}

	.title_image image {
		width: 98%;
		margin-left: 1%;
		height: 170rpx;
	}

	.member_content {
		margin-top: 30rpx;
		background-color: #FFFFFF;
		height: 370rpx;
		padding-top: 20rpx;
		text-align: center;
		color: #555555;
	}

	.content_title {
		font-size: 32rpx;
		font-weight: 600;
	}

	.content_title2 {
		font-size: 32rpx;
		margin-top: 30rpx;
		margin-bottom: 30rpx;
		font-weight: 500;
	}

	.content_title2 text {
		color: #F56160;
		margin-left: 10rpx;
	}

	.content_image image {
		width: 100%;
		height: 200rpx;
	}
	
	.member_txt{
		padding: 20rpx;
		color: #A2A2A2;
		font-size: 24rpx;
	}
	
	.member_btn{
		background-color: #FFFFFF;
		padding: 30rpx;
	}
	
	.member_btn button{
		background-color: #000000;
		color: #FFFFFF;
	}
</style>
