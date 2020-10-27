<template>
	<view class="contentContainer">
		<view class="leftContainer">
			<scroll-view scroll-y="true" class="leftScroll" >
				<view @click="changenavIndex(index)" class="navItem" :class='{active:navIndex===index}' v-for="(item,index) in categoryList" :key='item.id'>{{item.name}}</view>
				
			</scroll-view>
		</view>
		<view class="rightContainer">
			<scroll-view scroll-y="true" class="rightscroll">
					<view class="shopList">
						<view class="shopItem" v-for="shopItem in cateObj.subCateList" :key="shopItem.id">
							<image class="rightimg" :src="shopItem.wapBannerUrl" ></image>
							<text class="text">{{shopItem.name}}</text>
							<text class="text">￥{{shopItem.vipPrice}}</text>
							<text class="text1">添加订单</text>
						</view>
					</view>
			</scroll-view>
		</view>
	</view>
</template>
 
<script>
	import request from '../../utils/request.js'
	export default{
		data(){
			return {
				categoryList:[],
				navIndex:0,
			};
		},
		
		mounted() {
			this.getCateGoryData()
		},
		methods:{
			async getCateGoryData(){
				
				let categoryList = await request('/getCateGoryData')
				this.categoryList=categoryList.data
				console.log(categoryList)
			},
			changenavIndex(index){
				this.navIndex=index
			}
		},
		computed:{
		cateObj(){
			return this.categoryList[this.navIndex]
		}
		}
	}
	
	
		
</script>

<style lang="less">
.contentContainer{
		display: flex;
		border-top:1rpx solid #eee;
		
		.leftContainer{
			width: 20%;
			height: 500rpx;
			// background: #eee;
			.leftScroll{
				height: calc(100vh);
				.navItem{
					position: relative;
					height: 80rpx;
					line-height: 80rpx;
					font-size: 26rpx;
					text-align: center;
				}
				.active:before{
					position: absolute;
					top:10rpx ;
					left: 6rpx;
					content:'';
					width:2rpx;
				  height:60rpx;
					background: red;
				}
			}
			
		}
		.rightContainer{
			border-left: 1rpx solid #eee;
			padding: 0 10rpx;
			height: 500rpx;
			// background: green;
			width: 80%;
			height: 100%;
			margin-left: 40rpx;
			.rightscroll{
				height: calc(100vh);
				.shopItem{
					margin-top: 30rpx;
					.rightimg{
						width: 520rpx;
						height: 300rpx;
					}
					.text{
						color: #333333;
						font-size: 26rpx;
						text-align: end;
						display: block;
						margin-right: 30rpx;
					}
					.text1{
						margin-left: 430rpx;
						color: white;
						width: 80rpx;
						height: 30rpx;
						background: red;
						text-align: end;
						border-radius: 8rpx;
						font-size: 20rpx;
						cursor: pointer;
						padding: 0 5rpx;
					
					}
				}
				
			}
		}
	
}
</style>
