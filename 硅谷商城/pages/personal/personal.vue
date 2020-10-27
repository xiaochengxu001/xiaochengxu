<template>
	<view class="container">
		<view class="header"  @click="toLogin">
			<image class="avatar" :src="userInfo.avatarUrl? userInfo.avatarUrl:'../../static/images/personal/personal.png'" />
			<p class="nickname">{{userInfo.nickName?userInfo.nickName:'未登录'}}</p>
		</view>
		<view class="section">
			<view class="line judgement">我的评价</view>
			<view class="line judgement">我的好友</view>
			<view class="line judgement">我的收藏</view>
			<view class="line judgement">我的地址 </view>
		</view>
		<view class="section">
			<view class="line judgement">我的钱包<text class="tl">余额：￥99999999999</text></view>
		</view>
		<view class="section">
			<view class="line judgement">邀请有奖</view>
			<view class="line judgement">商家入驻</view>
		</view>
		<view class="section">
			<view class="line judgement">帮助与反馈</view>
			<view class="line judgement">在线客服<text class="tl">9:00 - 23:00</text></view>
		</view>
		
	</view>
	
</template>

<script>
	export default{
		data() {
			return {
				//存储用户信息
				userInfo:{}
				}
			
		},
		mounted(){
			wx.getUserInfo({
				success: (res) => {
					console.log(res);
					this.userInfo = res.userInfo;
				},
				fail: (err) => {
					console.log('获取用户信息失败')
				}
			})
			},
		methods:{
			toLogin(){
				wx.navigateTo({
					url:'/pages/login/login'
				})
			}
		}

	}
</script>

<style lang="less" scoped>
	.header {
		background: #feb70f;
		padding: 30rpx;
	}
	.header .avatar {
		display: block;
		margin: 0 auto;
		width: 160rpx;
		height: 160rpx;
		border-radius: 50%;
		border: 2px solid #fee767;
	}
	.header .nickname {
		color: #000;
		font-size: 22px;
		line-height: 2.4;
		text-align: center;
		letter-spacing:10rpx;
	}
	
	.section {
		padding: 0;
		color: #2e2e2e;
		font-size: 30rpx;
	}
	.section .line {
		margin-left: 30rpx;
		padding-right: 30rpx;
		line-height: 3;
		border-bottom: 1px solid #efefef;
	}
	.section .line:last-child {
		border-bottom: none;
	}
	.section .line:before {
		content: '>';
		float: right;
		color: #aaa;
		margin-left: 20rpx;
	}
	.section .line .tl {
		float: right;
		color: #aaa;
	}
	
</style>
