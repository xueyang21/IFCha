<template>
	<view class="IFCha_submit">
		<view class="submit_head">
			<!-- 头部白色内容开始 -->
			<view class="head_content">
				<view class="content_title">
					到店自取
				</view>
				<view class="content_address">
					自取地址
					<view class="address_txt">
						学院街30号L6商铺
					</view>
					<view class="address_map" @click="getLocation">
						查看地图
					</view>
				</view>
				<view class="msg_date" @click="clickNavi">
					<text>自取时间</text>
					<text class="date_txt">{{ date }}日12:00</text>
				</view>
				<view class="msg_date">
					<text>自取电话</text>
					<text class="date_txt">请输入自取联系人电话</text>
				</view>
				<view class="msg_date">
					<text>自取联系人</text>
					<text class="date_txt">请输入自取联系人</text>
				</view>
				<view class="msg_date">
					<view class="data_checkbox">
						<van-checkbox @change="onChange" :value="checked"></van-checkbox>
					</view>
					<text>同意</text>
					<text class="date_text">《到店自取服务协议》</text>
				</view>
			</view>
			<!-- 头部白色内容结束 -->
			<view class="submit_shop">
				<view class="shop_title">
					IFCha一夫茶
				</view>
				<view class="shop_content">
					<image :src="shop.bz_1" mode=""></image>
					<view class="content_shop">
						<view class="shop_txt1">
							{{ shop.name }}
						</view>
						<view class="shop_txt2">
							x{{ shop.num }}
						</view>
					</view>
					<view class="content_price">
						￥{{ shop.price }}.00
					</view>
				</view>
			</view>
			<!-- 实付款开始 -->
			<view class="submit_money">
				<view class="msg_date">
					<text>实付款</text>
					<text class="date_proces">小计<text>￥{{ shop.prices }}.00</text> </text>
					<text class="data_money">{{ discount }}</text>
				</view>
			</view>
			<!-- 实付款结束 -->
			<view class="tab_submit">
				<view class="">
					<text class="submit_txt1">{{ discount }}</text>
					<text class="submit_txt2">合计<text>￥{{ shop.prices }}.00</text> </text>
					<button type="submit" @click="submit">提交订单</button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				date: new Date().toISOString().slice(0, 10),
				checked: true,
				shop: {},
				discount:'已优惠￥0.00'
			}
		},
		onLoad(option) {
			console.log(option)
			this.shop = option
		},
		methods: {
			clickNavi() {
				uni.navigateTo({
					url: '../index/time'
				})
			},
			onChange(e) {
				this.checked = e.detail
			},
			submit() {
				uni.showToast({
				  title: '提交成功',
				  icon: 'success',
				  duration: 2000
				})
			},
			getLocation() {
				let _this = this
				uni.openLocation({
					latitude: 35.321421,
					longitude: 113.909258,
					name: 'IFCha一夫茶（万达店）',
					address: '学院街30号L6商铺',
					success: function(res) {
						console.log(res);
					}
				});
			}
		}
	}
</script>

<style scoped>
	.IFCha_submit {
		width: 100%;
		background-color: #EEEEEE;
	}

	.submit_head {
		width: 100%;
		height: 300rpx;
		float: left;
		background-color: #000000;
	}

	.head_content {
		width: 90%;
		margin-left: 5%;
		background-color: #FFFFFF;
		padding-top: 15rpx;
		border-top-right-radius: 40rpx;
		border-top-left-radius: 40rpx;
	}

	.content_title {
		text-align: center;
		font-size: 34rpx;
		font-weight: 600;
		border-bottom: 1rpx solid #EEEEEE;
		padding-bottom: 15rpx;
	}

	.content_address {
		padding: 40rpx 20rpx 40rpx 20rpx;
		text-align: center;
		border-bottom: 1rpx solid #EEEEEE;
	}

	.address_txt {
		font-size: 32rpx;
		padding-top: 15rpx;
		padding-bottom: 15rpx;
	}

	.address_map {
		color: #3DADFE;
	}

	.msg_date {
		padding: 25rpx;
		border-bottom: 1rpx solid #EEEEEE;
		font-size: 16px;
	}

	.date_txt {
		float: right;
		margin-top: 5rpx;
		color: #8F8F8F;
	}

	.data_checkbox {
		float: left;
		margin-right: 20rpx;
	}

	.date_text {
		color: #54B8FF;
	}

	.submit_shop {
		margin-top: 20rpx;
		background-color: #FFFFFF;
		width: 90%;
		margin-left: 5%;
		padding-top: 15rpx;
	}

	.shop_title {
		text-align: center;
		font-size: 32rpx;
		font-weight: 600;
		padding-bottom: 15rpx;
		color: #676767;
	}

	.shop_content {
		background-color: #F8F8F8;
		padding: 20rpx;
	}

	.shop_content image {
		width: 120rpx;
		height: 120rpx;
		float: left;
		margin-right: 20rpx;
	}


	.shop_txt1 {
		margin-bottom: 55rpx;
		color: #565656;
	}

	.shop_txt2 {
		color: #A9A9A9;
	}

	.content_price {
		float: right;
		margin-top: -30rpx;
	}

	.submit_money {
		margin-top: 20rpx;
		background-color: #FFFFFF;
		width: 90%;
		margin-left: 5%;
	}

	.data_money {
		float: right;
		margin-right: 20rpx;
	}

	.date_proces {
		float: right;
		margin-top: -10rpx;
	}

	.date_proces text {
		font-size: 38rpx;
		color: #E90000;
		font-weight: 600;
	}

	.tab_submit {
		position: fixed;
		bottom: 0;
		width: 100%;
	}

	.tab_submit view {
		display: flex;
		flex: 1;
		background-color: #FFFFFF;
	}

	/* .tab_submit text {
		font-size: 34rpx;
		padding-top: 25rpx;
		padding-left: 50rpx;
	} */
	
	.submit_txt1{
		width: 38%;
		font-size: 28rpx;
		padding-top: 25rpx;
		padding-left: 20rpx;
		color: #A2A2A2;
	}

	.submit_txt2{
		width: 32%;
		font-size: 28rpx;
		padding-top: 25rpx;
		padding-left: 50rpx;
		margin-top: -6rpx;
	}
	.submit_txt2 text{
		color: #E90000;
		font-weight: 600;
		font-size: 34rpx;
	}

	.tab_submit button {
		width: 30%;
		background-color: #000000;
		color: #FFFFFF;
	}
</style>
