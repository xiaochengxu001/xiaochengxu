
	<template>
		<view class="loginContainer">
			<image class="logo" src="../../static/images/logo/2.jpg"  mode=""></image>
		
			<div class="loginMethods">
				<button class="login wechatLogin" open-type="getUserInfo" @getuserinfo='handleGetUserInfo'>
					微信登录
				</button>
			</div>
		</view>
	</template>



<script>
	export default {
		data() {
			return {
				
			}
		},
		methods:{
			handleGetUserInfo(res){
				console.log(res)
				if(res.detail.userInfo){ // 用户授权
					wx.setStorage({
						key: 'userInfo',
						data: JSON.stringify(res.detail.userInfo)
					})
					wx.reLaunch({
						url: '/pages/personal/personal'
					})
				
			}
			
		}
		}
		
	}
	
</script>

<style lang="stylus" scoped>
	.loginContainer
		width 100%
		height 100%
		background #F8F8F8
		display flex
		align-items center
		flex-direction column
		.logo
			width 400upx
			height 533upx
			margin-top 200upx
		.loginMethods
			width 80%
			margin 150upx auto
			display flex
			justify-content space-around
			.login
				width 240upx
				height 80upx
				background #41A863
				color #FFFFFF
				text-align center
				line-height 80upx
				font-size 40upx
			
</style>
