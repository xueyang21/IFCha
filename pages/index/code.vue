<template>
	<view class="" >
		<view class="" >
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				
			}
		},
		onLoad() {
			this.scanCode()
		},
		methods: {
			scanCode() {
				// 允许从相机和相册扫码
				uni.scanCode({
					success: function(res) {
						console.log(res);
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
						console.log('1')
						uni.navigateBack({
							delta:1
						})
					},fail(ress){
						console.log(ress)
						uni.navigateBack({
							delta:1
						})
					}
				})
			}
		}
	}
</script>

<style>
</style>
