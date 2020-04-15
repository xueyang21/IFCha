<template>
	<view class="IFCha_address">
		<view class="" @tap="openMap">

		</view>
		<view class="address_box">
			<view class="address_btn">
				<button class="btn1" type="default" @click="clickNavi">手动添加</button>
				<button class="btn2" type="default" @click="clickNavi2">微信添加</button>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
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
	.address_box{
		width: 100%;
		position: fixed;
		bottom: 0;
	}
	.address_btn{
		display: flex;
		flex-wrap: wrap;
		flex: 1;
	}
	.address_btn button{
		width: 45%;
	}

</style>
