<template>
	<view class="IFCha_take">
		<!-- 头像部分开始 -->
		<view class="take_head">
			<image class="head_img1" src="../../static/image/qq.jpg" mode=""></image>
			<view class="head_content">
				<view class="content_title">IFCha一夫茶</view>
				<view class="content_new">
					<image src="../../static/image/broadcast.png" mode=""></image>
					<text>新用户下单，立减5元</text>
				</view>
				<view class="content_song" @tap="showModal" data-target="Image">￥20起送 | 送达 | 商家配送（8公里内）<text>></text></view>
			</view>
		</view>
		<!-- 头像部分结束 -->
		<!-- tab开始 -->
		<van-tabs active="a">
			<van-tab title="外卖点餐" name="a">
				<view class="tab_content1">
					<view class="content1" @tap="showModal" data-target="Image">
						<image src="../../static/image/new.png" mode=""></image>
						<text>新用户下单立减5.00元(不与其它活动共享)
							<text>▼</text>
						</text>
					</view>
					<!-- 商品列表开始 -->
					<van-sidebar style="float: left;">
						<van-sidebar-item v-for="i in list" :key="i" :title="i.name" @click="mym(i.id)" />
					</van-sidebar>
					<van-card v-for="(i,index) in arr" :key="i" :price="price" desc="月销666笔" origin-price="30.00" :title="i.name"
					 :thumb="i.bz_1">
						<view slot="footer">
							<van-stepper :value="value" @change="onChange1" @plus="onPlus(i,index)" />
						</view>
					</van-card>
					<view class="tab_submit">
						<view class="">
							<text>￥{{ prices }}.00</text><button type="default" @click="clickNavi">去结算</button>
						</view>
					</view>
					<!-- 商品列表结束 -->
				</view>
			</van-tab>
			<van-tab title="评价" name="b">
				<view class="tab_content2">
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
			<van-tab title="详情" name="c">
				<view class="tab_content3">
					<view class="content3_cell1">
						<view class="content3_cell">
							<van-cell style="font-size: 16px;" title="商家名称" value="IFCha一夫茶" />
						</view>
						<view class="content3_cell">
							<van-cell title="电话" is-link value="15334457200" />
						</view>
						<view class="content3_cell">
							<van-cell title="地址" is-link value="宣威市文化路沃尔玛停车场上行30米左右" />
						</view>
						<view class="">
							<van-cell title="营业时间" value="12:00-23:00" />
						</view>
					</view>

					<view class="content_setting">
						<view class="setting1">商家环境</view>
						<view class="setting2">商家暂未上传图片</view>
						<view class="setting1">商家资质</view>
						<view class="setting2">商家暂未上传资质</view>
					</view>
					<view class="content_summary">
						<view>商家简介</view>
						<image src="../../static/image/qq.jpg" mode=""></image>
					</view>
					<button class="content_btn" type="default">举报商家</button>
				</view>

			</van-tab>
		</van-tabs>
		<!-- tab结束 -->

		<view class="cu-modal" :class="modalName=='Image'?'show':''">
			<view class="cu-dialog">
				<view class="bg-img" style="background-image: url('https://ossweb-img.qq.com/images/lol/web201310/skin/big91012.jpg');height:200px;">
					<view class="cu-bar justify-end text-white">
						<view class="action" @tap="hideModal">
							<text class="cuIcon-close "></text>
						</view>
					</view>
				</view>
				<view class="cu-bar bg-white">
					<view class="action margin-0 flex-sub  solid-left" @tap="hideModal">我知道了</view>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				activeKey: 0,
				checked: false,
				modalName: null,
				list: [],
				arr: [],
				price: 15.00,
				value: 0,
				num: 0,
				numb: 0,
				prices: 0,
				plusList:{}
			}
		},
		onLoad() {
			this.leftList()
			this.mym(2)
		},
		methods: {
			onChange(event) {
				console.log(event)
				this.checked = event.detail
			},
			showModal(e) {
				this.modalName = e.currentTarget.dataset.target
			},
			hideModal(e) {
				this.modalName = null
			},
			leftList() {
				var _this = this;
				uni.request({
					url: "https://wxmall.xingyuncm.cn/api/Category/index",
					success(res) {
						console.log(res)
						_this.list = res.data.list;
					}
				})
			},
			mym(id) {
				var _this = this;
				uni.request({
					url: "https://wxmall.xingyuncm.cn/api/Category/getcat",
					data: {
						cat_id: id
					},
					success(res) {
						console.log(res);
						_this.arr = res.data.catList;
					}
				})
			},
			onChange1(e) {
				let _this = this
				console.log(e.detail)
				_this.num = e.detail
				_this.prices = _this.num * _this.price
			},
			onPlus(e) {
				console.log(e)
				this.plusList = e
			},
			clickNavi(){
				let _this = this;
				let price = _this.price; //单价
				let prices = _this.prices; //总价
				let name = _this.plusList.name; //商品名字
				let bz_1 = _this.plusList.bz_1; //商品图片
				let num = _this.num //商品数量
				uni.navigateTo({
					url:"../index/submit?price=" + price + "&prices=" + prices + "&name=" + name + "&bz_1=" + bz_1 + "&num=" + num
				})
			}
		}
	}
</script>

<style scoped>
	.IFCha_take {
		background-color: #F4F4F4;
		width: 100%;
		height: 1800rpx;
	}

	.take_head {
		background-color: #000000;
		padding: 60rpx 30rpx 60rpx 30rpx;
	}

	.head_img1 {
		float: left;
		width: 120rpx;
		height: 120rpx;
		border-radius: 50%;
		border: solid 2px #D1B452;
		margin-right: 30rpx;
		margin-top: 16rpx;
	}

	.head_content {
		color: #FFFFFF;
	}

	.content_title {
		font-size: 32rpx;
		font-weight: 600;
	}

	.content_new image {
		float: left;
		width: 35rpx;
		height: 35rpx;
		margin-right: 10rpx;
		margin-top: -5rpx;
	}


	.content_new {
		font-size: 20rpx;
		margin-top: 25rpx;
		margin-bottom: 25rpx;
	}

	.content_song {
		font-size: 23rpx;
	}

	.content_song text {
		float: right;
		margin-top: -5rpx;
		font-size: 30rpx;
		font-weight: 600;
	}

	.content1 {
		background-color: #FFFFFF;
		padding: 15rpx 20rpx;
	}

	.content1 image {
		float: left;
		width: 40rpx;
		height: 40rpx;
		margin-right: 20rpx;
	}

	.content1 text {
		margin-top: 5rpx;
		color: #A8A8A8;
	}

	.content1 text text {
		float: right;
		color: #727272;
		font-size: 36rpx;
		margin-top: -5rpx;
	}

	.tab_content2 {
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

	.tab_content3 {
		margin-top: 20rpx;
	}

	.content_setting {
		margin-top: 20rpx;
		background-color: #FFFFFF;
		padding: 20rpx 0 5rpx 30rpx;
	}

	.setting1 {
		font-size: 34rpx;
		margin-bottom: 20rpx;
		color: #555555;
	}

	.setting2 {
		font-size: 26rpx;
		margin-bottom: 40rpx;
		margin-left: 30rpx;
		color: #595959;
	}

	.content_summary {
		margin-top: 20rpx;
		padding: 20rpx;
		background-color: #FFFFFF;
		font-size: 34rpx;
		color: #555555;
	}

	.content_summary image {
		width: 100%;
		margin-right: 20rpx;
		height: 700rpx;
	}

	.content_btn {
		width: 90%;
		margin: 30rpx 5% 30rpx 5%;
		background-color: #FFFFFF;
	}

	.content2_js image {
		width: 140rpx;
		height: 140rpx;
	}

	.content3_cell {
		border-bottom: 1rpx solid #EEEEEE;
	}

	.content3_cell1 {
		background-color: #FFFFFF;
	}

	.tab_submit {
		position: fixed;
		bottom: 0;
		width: 100%;
		z-index: 9999;
	}

	.tab_submit view {
		display: flex;
		flex: 1;
		background-color: #FFFFFF;
	}

	.tab_submit text {
		font-size: 34rpx;
		width: 70%;
		padding-top: 25rpx;
		padding-left: 50rpx;
	}

	.tab_submit button {
		width: 30%;
		background-color: #000000;
		color: #FFFFFF;
	}
</style>
