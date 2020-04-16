<template>
	<view class="IFCha_ship">
		<view class="ship_head" @click="clickNavi" v-show="show">
			<view class="head_view1">
				{{ add.userName }},{{add.telNumber}}
			</view>
			<view class="">
				{{ add.provinceName }} {{ add.cityName }} {{ add.countyName }} {{ add.detailInfo }}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				add:{},
				show:false
			}
		},
		onLoad() {
			let _this = this
			uni.getSetting({
				success(res) {
					console.log(res)
					console.log("vres.authSetting['scope.address']：", res.authSetting['scope.address'])
					if (res.authSetting['scope.address']) {
						console.log("111")
						uni.chooseAddress({
							success(res) {
								console.log(res)
								console.log(res.userName)
								console.log(res.postalCode)
								console.log(res.provinceName)
								console.log(res.cityName)
								console.log(res.countyName)
								console.log(res.detailInfo)
								console.log(res.nationalCode)
								console.log(res.telNumber)
								_this.add = res
								
								if (Object.keys(res).length === 0) {
									return _this.show = false // 如果为空,返回false
								}
								return _this.show = true
							}
						})
						// 用户已经同意小程序使用录音功能，后续调用 wx.startRecord 接口不会弹窗询问

					} else {
						if (res.authSetting['scope.address'] == false) {
							console.log("222")
							uni.openSetting({
								success(res) {
									console.log(res.authSetting)

								}
							})
						} else {
							console.log("eee")
							uni.chooseAddress({
								success(res) {
									console.log(res.userName)
									console.log(res.postalCode)
									console.log(res.provinceName)
									console.log(res.cityName)
									console.log(res.countyName)
									console.log(res.detailInfo)
									console.log(res.nationalCode)
									console.log(res.telNumber)
								}
							})
						}
					}
				}
			})
		},
		methods: {
			clickNavi(){
				let _this = this;
				let addName = _this.add.detailInfo
				let addAdd = _this.add.provinceName + _this.add.cityName + _this.add.countyName
				let name = _this.add.userName
				let tel = _this.add.telNumber
				let value = ''
				uni.navigateTo({
					url:"./address?addName=" + addName + "&addAdd=" + addAdd + "&value=" + value + "&name=" + name + "&tel=" + tel,
				})
			}
		}
	}
</script>

<style>
	.ship_head{
		padding: 25rpx;
	}
	.head_view1{
		margin-bottom: 20rpx;
	}
</style>
