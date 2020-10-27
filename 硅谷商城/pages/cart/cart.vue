<template>
	<view class="cartContainer">
		<block v-if="!userInfo.nickName">
			<view class="contentContainer">
				<image class="cartImg" src="http://yanxuan-static.nosdn.127.net/hxm/yanxuan-wap/p/20161201/style/img/icon-normal/noCart-d6193bd6e4.png?imageView&type=webp" mode=""></image>
				<button @click="toLogin">登录</button>
				<view class="addMore">去添加点什么吧</view>
			</view>
		</block>
		<block v-else>
		<!-- 购物车列表 -->
			<block v-if="cartList.length">
				<view class="clear">
					<view class="" style="font-size: 35rpx;">
						x
					</view>
					<view class="" style="margin-top: 10rpx;">
						清空
					</view>
				</view>
				<view class="cartList">
					<view class="cartItem" v-for="(shopItem, index) in cartList" :key='shopItem.id'>
						<view class="shopItem">
							<text>{{shopItem.name}}</text>
							<text class="price">￥{{shopItem.retailPrice}}</text>
						</view>
						<!-- 控制数量 -->
						<view class="countCtrl">
							<text class="add" @click="changCount(true, index)"> + </text>
							<text class="count"> {{shopItem.count}} </text>
							<text class="del" @click="changCount(false, index)"> - </text>
						</view>
					</view>
				</view>
				<!-- 底部下单 -->
				<view class="cartFooter">
					<image src="../../static/images/carts/emptyCart.gif" mode=""></image>
					<view class="right">
						<text class="totalPrice">合计: ￥{{totalPrice}}</text>
						<text class="preOrder">去结算</text>
					</view>
				</view>
			</block>	
			</block>
		<block v-else>
			<image class="cartImg" src="http://yanxuan-static.nosdn.127.net/hxm/yanxuan-wap/p/20161201/style/img/icon-normal/noCart-d6193bd6e4.png?imageView&type=webp" mode=""></image>
			<view class="hint">购物车还是空的，赶紧去购物吧</view>
		</block>
			
		<!-- </block> -->
	</view>
</template>

<script>
	import {mapState, mapMutations, mapGetters} from 'vuex'
	export default {
		data() {
			return {
				person: {
					username: 'curry'
				},
				userInfo: {}
			};
		},
		computed: {
			...mapState({
				cartList: state => state.cart.cartList
			}),
			...mapGetters(['isAllSelected', 'totalCount', 'totalPrice'])
		},
		mounted() {
			// 非响应式属性
			// this.person.age = 38
			let userInfo = wx.getStorageSync('userInfo');
			if(userInfo){
				this.userInfo = JSON.parse(userInfo)
			}
			
		},
		methods: {
			...mapMutations({
				changeCountMutation: 'changeCountMutation',
				changeAllSelectedMutation: 'changeAllSelectedMutation'
			}),
			changCount(isAdd, index){
				this.changeCountMutation({isAdd, index});
			},
			changeAllSelecte(allSelected){
				this.changeAllSelectedMutation(allSelected);
			},
			toLogin(){
				wx.reLaunch({
					url: '/pages/login/login'
				})
			}
		}
	}
</script>

<style lang="stylus">
	.cartContainer
		position relative
		background #f4f4f4
		height 100%
		.contentContainer
			.cartImg
				width 500rpx
				height 400rpx
				display block
				margin 0 auto
				padding-top 100rpx
			button
				width 480upx
				height 92upx
				background #DD1A21
				color #fff
				font-size 32upx
				line-height 92upx
			.addMore
				text-align center
				font-size 26upx
				color #7f7f7f
				line-height 60rpx
		.clear
			font-size 24rpx
			margin 5rpx 50rpx
			//margin-top 10rpx
			display flex
			justify-content space-between
		.cartList
			//margin-bottom 96rpx
			overflow hidden
			.cartItem
				position relative
				display flex
				justify-content space-between
				//height 100upx
				background #fff
				margin-top 20upx
				padding 20upx
				.shopItem
					float left
					font-size 28upx
					flex-direction column
					margin-left 20upx
					text
						line-height 60upx
				.price
					color: #BB2C08
					margin-left 200rpx
				.countCtrl
					position absolute
					right 20upx
					bottom 30upx
					text
						display inline-block
						width 60upx
						height 50upx
						text-align center
						line-height 50upx
						border 1upx solid #EEEEEE
						&:nth-child(2)
							border none
							border-top 1upx solid #EEEEEE
							border-bottom 1upx solid #EEEEEE
		.cartFooter
			position fixed
			display flex	
			bottom 0rpx
			height 96upx
			line-height 96upx
			width 100%
			background #fff
			font-size 30upx
			image
				width 100rpx
				height 100rpx
				font-size 40upx
				margin 0 40upx
				color: #999
				&.selected
					color: #BB2C08
			.right 
				height 96upx
				position absolute
				right 0
				.totalPrice
					display inline-block
					height 96upx
					line-height 96upx
				.preOrder
					display inline-block
					background #DD1A21
					width 225upx
					height 96upx
					line-height 96upx
					text-align center
					font-size 28upx
					color #fff
					margin-left 30upx
		.hint
			text-align center
			font-size 28upx
					
</style>
