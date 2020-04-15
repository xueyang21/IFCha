<template>
	<view class="IFCha_reserve">
		<!-- 预约信息开始 -->
		<view class="reserve_msg">
			<view class="msg_title">
				<view class="title1"></view>
				<text class="title2">预约信息</text>
			</view>
			<view class="msg_people">
				<view class="uni-list-cell-left">
					选择人数
				</view>
				<view class="uni-list-cell-db">
					<picker class="msg_picker" @change="bindPickerChange" :value="index" :range="array">
						<view class="uni-input">{{array[index]}}</view>
					</picker>
				</view>
			</view>
			<view class="msg_date" @click="clickNavi">
				<text>选择时间</text>
				<text class="date_txt">{{ date }}日12:00</text>
			</view>
			<view class="msg_people">
				<view class="uni-list-cell-left">
					选择桌位类型
				</view>
				<view class="msg_current">
					<picker class="" @change="clickPickerChange" :value="i" :range="array1">
						<text class="current_txt">--最低消费0.00</text><text class="current_input">{{array1[i]}}</text>
					</picker>
				</view>
			</view>
			<view class="msg_money">
				桌位预定费用<text>0.00元</text>
			</view>
			<view class="msg_person">
				<van-field :value="person" type="text" label="联系人" placeholder="请输入联系人称呼" />
			</view>
			<view class="msg_person">
				<van-field :value="phone" type="text" label="联系电话" placeholder="请输入电话号码" />
			</view>
		</view>
		<!-- 预约信息结束 -->
		<!-- 预约模式开始 -->
		<view class="reserve_mode">
			<view class="mode_title">
				<view class="title1"></view>
				<text class="title2">预约模式</text>
			</view>
			<van-radio-group :value="radio" @change="onChange">
				<van-cell-group>
					<van-cell class="mode1" title="只订座" clickable data-name="1" @click="onClick">
						<van-radio class="mode1_radio" slot="right-icon" name="1" />
					</van-cell>
					<van-cell class="mode2" title="提前选商品" clickable data-name="2" @click="onClick">
						<van-radio class="mode2_radio" slot="right-icon" name="2" />
					</van-cell>
				</van-cell-group>
			</van-radio-group>
		</view>
		<!-- 预约模式结束 -->
		<!-- 备注开始 -->
		<view :v-if="radio != 1" class="reserve_remark">
			备注
			<input type="text" value="" placeholder="请输入备注信息" />
		</view>
		<!-- 备注结束 -->
		<!-- 立即预约按钮开始 -->
		<view class="reserve_btn">
			<button type="default">立即预约</button>
		</view>
		<!-- 立即预约按钮结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				index: 0,
				array: ['1人', '2人', '3人', '4人', '5人', '6人', '7人', '8人', '9人', '10人', '10人以上'],
				date: new Date().toISOString().slice(0, 10),
				array1: ['食堂点餐', '沙发', '长桌', '双人桌'],
				i: 0,
				radio: '1'
			}
		},
		methods: {
			bindPickerChange: function(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
			},
			clickNavi() {
				uni.navigateTo({
					url: '../index/time'
				})
			},
			clickPickerChange(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.i = e.target.value
			},
			onChange(event) {
				this.radio = event.detail
			},

			onClick(event) {
				console.log(event)
				const {	name } = event.currentTarget.dataset;
				this.radio = name
			}
		}
	}
</script>

<style scoped>
	.IFCha_reserve {
		background-color: #F4F4F4;
	}

	.reserve_msg {
		background-color: #FFFFFF;
	}

	.msg_title {
		padding: 25rpx 0 25rpx 25rpx;
		border-bottom: 1rpx solid #EEEEEE;
	}

	.title1 {
		width: 10rpx;
		height: 50rpx;
		float: left;
		background-color: #000000;
		margin-right: 20rpx;
	}

	.title2 {
		font-size: 34rpx;
	}

	.uni-list-cell-left {
		float: left;
	}

	.msg_people {
		padding: 25rpx;
		border-bottom: 1rpx solid #EEEEEE;
		font-size: 16px;
		height: 90rpx;
	}

	.uni-list-cell-db {
		float: right;

	}

	.uni-input {
		float: right;
	}

	.msg_date {
		padding: 25rpx;
		border-bottom: 1rpx solid #EEEEEE;
		font-size: 16px;
	}

	.date_txt {
		float: right;
		margin-top: 5rpx;
	}

	.current_input {
		float: right;
	}

	.current_txt {
		float: right;
	}

	.msg_money {
		padding: 25rpx;
		font-size: 16px;
		border-bottom: 1rpx solid #EEEEEE;
	}

	.msg_money text {
		float: right;
	}

	.msg_person {
		font-size: 16px;
		border-bottom: 1rpx solid #EEEEEE;
	}

	.reserve_mode {
		margin-top: 40rpx;
		background-color: #FFFFFF;
		height: 280rpx;
	}

	.mode_title {
		padding: 25rpx 0 50rpx 25rpx;
	}

	.mode1 {
		float: left;
		width: 45%;
		border-radius: 15rpx;
		margin-left: 3%;
		margin-right: 3%;
		background-color: #000000;
		color: #FFFFFF;
		padding: 20rpx 0;
	}

	.mode2 {
		float: left;
		width: 45%;
		border-radius: 15rpx;
		background-color: #000000;
		color: #FFFFFF;
		padding: 20rpx 0;
	}

	.mode1_radio {
		margin-left: 50%;
		margin-top: 10rpx;
	}

	.mode2_radio {
		margin-left: 30%;
		margin-top: 10rpx;
	}
	
	.reserve_remark {
		padding: 30rpx;
		margin-top: 40rpx;
		background-color: #FFFFFF;
		height: 280rpx;
		margin-bottom: 80rpx;
	}
	.reserve_remark input{
		height: 150rpx;
		border: 1rpx solid #EEEEEE;
		margin-top: 10rpx;
		padding: 20rpx;
	}
	
	.reserve_btn{
		padding: 20rpx 30rpx;
		background-color: #FFFFFF;
		bottom: 0;
		width: 100%;
		position: fixed;
	}
	.reserve_btn button{
		background-color: #000000;
		color: #FFFFFF;
	}
</style>
