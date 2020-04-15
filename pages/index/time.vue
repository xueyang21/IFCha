<template>
	<view class="IFCha_time">
		<view class="time_head">
			<view class="head_content">
				<view class="">今天</view>
				<text>{{ date }}</text>
			</view>
		</view>
		<view class="time_content">
			已选日期：{{ date }}
		</view>
		<view class="time_btn">
			<button type="default">立即预约</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				date: new Date().toISOString().slice(0, 10),
			}
		}
	}
</script>

<style>
	.IFCha_time {
		background-color: #F4F4F4;
	}

	.time_head {
		height: 150rpx;
		text-align: center;
		background-color: #FFFFFF;
	}

	.head_content {
		width: 180rpx;
		padding: 40rpx 0 30rpx 0;
		border-bottom: 5rpx solid #000000;
	}

	.head_content view {
		font-weight: 600;
		margin-bottom: 10rpx;
	}

	.head_content text {
		font-weight: 600;
	}

	.time_content {
		padding: 25rpx;
	}

	.time_btn {
		padding: 20rpx 30rpx;
		background-color: #FFFFFF;
		bottom: 0;
		width: 100%;
		position: fixed;
	}

	.time_btn button {
		background-color: #000000;
		color: #FFFFFF;
	}
</style>
