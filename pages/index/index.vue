<template>
	<view class="IFCha_index">
		<!-- 轮播开始 -->
		<swiper class="index_swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
			<swiper-item v-for="banner in banners" :key="index">
				<image class="index_banner" :src="banner.photo" mode=""></image>
			</swiper-item>
		</swiper>
		<!-- 轮播结束 -->
		<!-- 点餐开始 -->
		<view class="index_take">
			<view class="take" v-for="(take,index) in takes" @click="clickNavi(take,index)">
				<view class="take_left">
					<view> {{ take.view }} </view>
					<text>{{ take.text }}</text>
				</view>
				<view class="take_right">
					<image :src=take.img mode=""></image>
				</view>
			</view>
		</view>
		<!-- 点餐结束 -->
		<!-- 商家详情开始 -->
		<view class="index_details">
			<view class="details_top">
				<image :src="details" mode=""></image>
				<text>商家详情</text>
			</view>
			<view style="clear: both;"></view>
			<view class="details_present">
				<image src="../../static/image/qq.jpg" mode=""></image>
				<view class="present_txt">
					<view>IFCha一夫茶</view>
					<text>￥15/人</text>
				</view>
				<view class="present_status">
					<view class="status1">店铺状态</view>
					<view class="status2">营业中</view>
				</view>
			</view>
			<view style="clear: both;"></view>
			<view class="details_content">
				<view class="content_time">
					<image src="../../static/image/time.png" mode=""></image>
					<text>营业时间：12：00-23：00</text>
				</view>
				<view class="content_dress">
					<image src="../../static/image/dress.png" mode=""></image>
					<text>宣威市文化路沃尔玛停车场上行30米左右</text>
					<view class="dress">
						<view class="dress_navi" @click="getLocation">
							<image src="../../static/image/navi.png" mode=""></image>
							<view>导航</view>
						</view>
						<view class="dress_phone" @click="makePhoneCall">
							<image src="../../static/image/phone.png" mode=""></image>
							<view>电话</view>
						</view>
					</view>
				</view>
				<view class="content_setting" @click="clickNavi2()">
					<image src="../../static/image/huanjing.png" mode=""></image>
					<text>商家环境<text style="float: right;">></text> </text>
				</view>
			</view>
		</view>
		<!-- 商家详情结束 -->
		<!-- Tab开始 -->
		<van-tabs active="a">
			<van-tab title="商品推荐" name="a">
				<view class="tab1_content">
					<image src="../../static/image/qq.jpg" mode=""></image>
					<view class="content_price">
						<view class="price1">满杯红柚</view>
						<view class="price2">￥18.00元<text>￥21.00元</text></view>
						<view class="price3">
							<text class="price3_txt1">8.6折</text>
							<text class="price3_txt2">会员价：￥17.00</text>
						</view>
					</view>
					<view class="content_once">
						<button type="default" @click="clickNavi1()">马上抢</button>
						<view>已销666份</view>
					</view>
				</view>
			</van-tab>
			<van-tab title="优惠券" name="b">
				<view class="tab2_content">
					暂无优惠券
				</view>
			</van-tab>
			<van-tab title="评价" name="c">
				<view class="tab3_content">
					<view class="content_score">
						综合评分 <text>0.0分</text>
					</view>
					<view class="content_select">
						<button type="default">全部0</button>
						<button type="default">满意0</button>
						<button type="default">不满意0</button>
					</view>
					<van-checkbox :value="checked" @change="onChange">有图评价</van-checkbox>
					<view class="content_none">
						暂无相关数据
					</view>
				</view>
			</van-tab>
		</van-tabs>
		<!-- Tab结束 -->
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
						photo: require('../../static/image/qq4.jpg')
					},
					{
						photo: require('../../static/image/qq4.jpg')
					}
				],
				takes: [{
						view: '外卖点餐',
						text: '首单立减5元',
						img: require('../../static/image/take.png'),
						path: "../index/take"
					},
					{
						view: '扫码点餐',
						text: '扫一扫轻松下单',
						img: require('../../static/image/code.png'),
						path: "../index/code"
					},
					{
						view: '预购',
						text: '预约免等待',
						img: require('../../static/image/rese.png'),
						path: "../index/rese"
					},
					{
						view: '付款',
						text: '无接触支付',
						img: require('../../static/image/payment.png'),
						path: "../index/payment"
					},
					{
						view: '抢购',
						text: '每日推出抢购商品',
						img: require('../../static/image/panic.png'),
						path: "../index/panic"
					},
					{
						view: '拼团',
						text: '参与拼团更优惠',
						img: require('../../static/image/fight.png'),
						path: "../index/fight"
					}
				],
				details: require('../../static/image/details.png'),
				checked: false
			}
		},
		onLoad() {
			let _this = this;
			// // 轮播
			// uni.request({
			// 	url: 'https://exam.qhynice.top/index.php/Api/Index/index',
			// 	data: {},
			// 	method: 'POST',
			// 	success(res) {
			// 		console.log(res.data.ggtop);
			// 		var banners = res.data.ggtop;
			// 		// console.log(banner);
			// 		_this.banners = banners;
			// 		console.log(_this.banners)
			// 	}
			// })
		},
		methods: {
			clickNavi(e) {
				console.log(e.path);
				var path = e.path;
				uni.navigateTo({
					url: path
				})
			},
			onChange(event) {
				console.log(event)
				this.checked = event.detail
			},
			clickNavi1() {
				uni.navigateTo({
					url: "../index/take"
				})
			},
			clickNavi2() {
				uni.navigateTo({
					url: '../index/setting'
				})
			},
			makePhoneCall() {
				uni.makePhoneCall({
					// 手机号
					phoneNumber: '18337396433',
					// 成功回调
					success: (res) => {
						console.log('调用成功')
					},
					// 失败回调
					fail: (res) => {
						console.log('调用失败')
					}
				})
			},
			getLocation() {
				uni.openLocation({
					latitude: 35.321421,
					longitude: 113.909258,
					name: 'IFCha一夫茶（万达店）',
					address: '学院街30号L6商铺',
					success: function() {
						console.log('success');
					}
				});
			}


		}
	}
</script>

<style scoped>
	.IFCha_index {
		height: 2000rpx;
		background-color: #F4F4F4;
	}

	.index_swiper {
		width: 100%;
		margin-bottom: 20rpx;
	}

	.index_banner {
		width: 100%;
		height: 300rpx;
	}

	.index_take {
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		flex: 2;
	}

	.take {
		margin: 0 2% 3% 2%;
		width: 46%;
		height: 140rpx;
		background-color: #FFF;
		border-radius: 15rpx;
	}

	.take_left {
		float: left;
		font-size: 28rpx;
		margin-top: 30rpx;
		margin-left: 20rpx;
		color: #555555;
	}

	.take_left text {
		font-size: 24rpx;
		color: #A1A1A1;
		display: inline-block;
		padding-top: 15rpx;
	}

	.take_right image {
		width: 90rpx;
		height: 90rpx;
		float: right;
		margin-top: 25rpx;
		margin-right: 20rpx;
	}

	.index_details {
		height: 560rpx;
		background-color: #FFF;
		padding-top: 20rpx;
		padding-left: 30rpx;
		margin-bottom: 20rpx;
		color: #5F5F5F;
	}

	.details_top image {
		width: 50rpx;
		height: 50rpx;
		margin-right: 20rpx;
		float: left;
	}

	.details_top text {
		display: inline-block;
		margin-top: 10rpx;
	}

	.details_present {
		width: 100%;
	}

	.details_present image {
		float: left;
		margin-top: 25rpx;
		width: 170rpx;
		height: 170rpx;
	}

	.present_txt {
		float: left;
		margin-top: 40rpx;
		margin-left: 25rpx;
	}

	.present_txt view {
		margin-bottom: 15rpx;
	}

	.present_status {
		float: right;
		width: 150rpx;
		height: 150rpx;
		background-color: #FC6167;
		margin-right: 40rpx;
		margin-top: 30rpx;
		color: #FFFFFF;
		text-align: center;
	}

	.status1 {
		margin-top: 10rpx;
		margin-bottom: 15rpx;
	}

	.status2 {
		width: 80%;
		margin-left: 10%;
		border-top: 1px solid #FFFFFF;
		font-size: 34rpx;
		padding-top: 20rpx;
	}

	.details_content {
		width: 95%;
	}

	.content_time {
		margin-top: 30rpx;
		padding-top: 20rpx;
		border-top: 1px solid #d9d9d9;
		border-bottom: 1px solid #d9d9d9;
		padding-bottom: 20rpx;
	}

	.content_time image {
		float: left;
		width: 35rpx;
		height: 35rpx;
		margin-top: 5rpx;
		margin-right: 10rpx;
	}

	.content_dress {
		padding-top: 20rpx;
		padding-bottom: 20rpx;
		border-bottom: 1px solid #d9d9d9;
	}

	.content_dress image {
		float: left;
		width: 22px;
		height: 22px;
		margin-right: 7rpx;
		margin-top: 15rpx;
	}

	.content_dress text {
		display: inline-block;
		width: 70%;
	}

	.dress {
		float: right;
	}

	.dress_navi {
		display: inline-block;
		font-size: 24rpx;
		border-right: 1px solid #d9d9d9;
		padding-right: 20rpx;
	}

	.dress_phone {
		display: inline-block;
		font-size: 24rpx;
		padding-left: 20rpx;
	}

	.content_setting {
		padding-top: 20rpx;
		padding-bottom: 20rpx;
	}

	.content_setting image {
		float: left;
		width: 35rpx;
		height: 35rpx;
		margin-right: 10rpx;
	}

	.tab1_content {
		margin-top: 20rpx;
		background-color: #FFFFFF;
		padding: 25rpx 0 25rpx 25rpx;
	}

	.tab1_content image {
		float: left;
		width: 170rpx;
		height: 170rpx;
		margin-right: 20rpx;
	}

	.content_price {
		display: inline-block;
		width: 350rpx;
		height: 170rpx;
	}

	.price1 {
		font-size: 32rpx;
		font-weight: 600;
	}

	.price2 {
		font-size: 38rpx;
		color: #F7656A;
		margin-top: 20rpx;
		margin-bottom: 25rpx;
	}

	.price2 text {
		font-size: 28rpx;
		color: #6C6C6C;
		margin-left: 20rpx;
		text-decoration: line-through;
	}

	.price3 {
		font-size: 22rpx;
	}

	.price3_txt1 {
		background-color: #FC6167;
		padding: 5rpx 10rpx 5rpx 10rpx;
		color: #FFFFFF;
	}

	.price3_txt2 {
		background-color: #F5ECB3;
		padding: 5rpx 10rpx 5rpx 10rpx;
		margin-left: 15rpx;
	}

	.content_once {
		display: inline-block;
		float: right;
		margin-right: 40rpx;
	}

	.content_once button {
		background-color: #FC6167;
		color: #FFFFFF;
		font-size: 30rpx;
		padding: 0 20rpx 0 20rpx;
		margin-top: 20rpx;
	}

	.content_once view {
		font-size: 25rpx;
		color: #F7656A;
		margin-top: 40rpx;
		margin-left: 10rpx;
	}

	.tab2_content {
		width: 100%;
		background-color: #FFFFFF;
		text-align: center;
		padding: 30rpx 0 30rpx 0;
	}

	.tab3_content {
		padding: 30rpx 0 20rpx 20rpx;
		background-color: #FFFFFF;
	}

	.content_score {
		color: #808080;
	}

	.content_score text {
		display: inline-block;
		font-size: 36rpx;
		color: #34B5FF;
		margin-left: 10rpx;
	}

	.content_select {
		margin-top: 30rpx;
		margin-bottom: 40rpx;
	}

	.content_select button {
		display: inline-block;
		width: 150rpx;
		padding: 0 10rpx 0 10rpx;
		font-size: 28rpx;
		margin-right: 20rpx;
		border-radius: 10rpx;
	}

	.content_none {
		text-align: center;
		color: #A5A5A5;
		margin-top: 20rpx;
	}
</style>
