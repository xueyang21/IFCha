<template>
	<view class="IFCha_edit">
		<view class="edit_field">
			<van-field value="" type="text" label="收货人" placeholder="姓名" />
		</view>
		<view class="edit_field">
			<van-field value="" type="text" label="联系电话" placeholder="手机号码" />
		</view>
		<view class="edit_field edit_field3">
			<view class="field_txt">
				<view class="">详细地址<text>\n</text>(门牌号)</view>
				<textarea :value="address.address + address.name" placeholder="输入地址或点击地图选择" />
				<image @click="openMap" src="../../static/image/dress.png" mode=""></image>
			</view>
		</view>
		<view class="edit_btn" >
			<button @click="save" type="default">保存</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				address:{
					address:'',
					name:''
				}
			}
		},
		onLoad() {
			var _this = this;
			uni.authorize({ // 发起请求用户授权
				scope: 'scope.userLocation',
				success() { // 用户允许了授权
					uni.getLocation({ // 请求位置信息
						type: 'gcj02',
						success(res) {
							console.log(res, 95); //  得到位置信息（经纬度，速度等等），====>>>>>请求附近门店
							
						}
					})
				}
			})
		},
		methods: {
			openMap: function() {
				var _this = this;
				uni.getLocation({
					type: 'gcj02', // 默认为 wgs84 返回 gps 坐标，gcj02 返回可用于 wx.openLocation 的坐标
					success: function(res) {
						console.log(res)
						uni.openLocation({
							latitude: res.latitude, // 纬度，范围为-90~90，负数表示南纬
							longitude: res.longitude, // 经度，范围为-180~180，负数表示西经
							scale: 18, // 缩放比例    
							success(res) {
								uni.chooseLocation({
									success(res) {
										console.log(res)
										_this.address = res
									}
								})
							}
						})
					}
				})
			},
			save(){
				uni.navigateTo({
					url:"./address"
				})
			}

		}
	}
</script>

<style scoped>
	.edit_field {
		padding-right: 20rpx;
		border-bottom: 1rpx solid #EEEEEE;
	}

.edit_field3{
	padding-right: 0;
}
	.edit_field3 image {
		width: 50rpx;
		height: 50rpx;
		float: right;
		margin-top: -70rpx;
	}
	.field_txt{
		padding: 20rpx 30rpx 20rpx 30rpx;
	}
	.field_txt view{
		float: left;
		width: 170rpx;
	}
	.field_txt textarea{
		color: #A5A6A8;
		height: 80rpx;
		margin-left: 170rpx;
		margin-top: -1rpx;
		width: 340rpx;
	}
	.edit_btn{
		width: 100%;
		padding: 20rpx;
		position: fixed;
		bottom: 0;
	}
</style>
