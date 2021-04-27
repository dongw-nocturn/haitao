<template>
	<view class="page">
		<scroll-view scroll-x class="bg-white nav" >
			<view class="flex text-center" style="padding-top: 7px;">
				<view style="position: relative;" class="cu-item flex-sub" :class="index==TabCur?'text-orange cur':''" v-for="(item,index) in filterType" :key="index" @tap="tabSelect" :data-id="index">
					{{item.title}}
					<text v-if="item.tips" class="cu-tag badge">{{item.tips}}</text>
				</view>
			</view>
		</scroll-view>
		<scroll-view style="height: 100%;" scroll-y="true" @scrolltolower="lower1" scroll-with-animation :scroll-into-view="toView">
			<view class='content'>
				<view class='card' v-for="(item,index) in list" v-if="list.length > 0" :key="index">
					<view class="border-title">
						{{item.shopName}}
						<text class="cuIcon-right"></text>
					</view>
					<view v-for="(shopItem,idx) in item.shopList" :key="idx" class="cardItem">
						<view class="flex">
							<image :src="shopItem.imageSrc" mode="aspectFit" class="shadow"></image>
							<view class="">
								<view class="">
									<text>{{shopItem.name}}</text>
									<text>{{shopItem.payMoney}}</text>
								</view>
								<text>创建时间:{{shopItem.createTime}}</text>
								<text>锁单时间:{{shopItem.clockTime}}</text>
								<text>支付时间:去支付订单</text>
							</view>
						</view>
						<view class="flex" style="justify-content: flex-end;">
							<button class="cu-btn round line-black margin-right-sm">再来一单</button>
							<button class="cu-btn round line-orange">分享得500积分</button>
						</view>
					</view>
				</view>
			</view>
			<view class='noCard' v-if="list.length===0">
				暂无信息
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				filterType:[
					{
						title:'全部',
						type:0,
					},
					{
						title:'待下单',
						type:1
					},
					{
						title:'待结算',
						type:2,
						tips:88
					},
					{
						title:'已结算',
						type:3
					},
					{
						title:'已作废',
						type:-1
					}
				],
				TabCur:0,
				currentTab: 0, //sweiper所在页
				toView:'',//回到顶部id
				list: [
					{
						shopName:'会员购北京',
						shopList:[{
							name:'肌肤之钥光凝前霜',
							createTime:'2021-09-01 19:22:03',
							clockTime:'2021-09-01 19:22:03',
							payTime:'2021-09-01 19:22:03',
							imageSrc:'../../static/logo.png',
							payMoney:99
						},
						{
							name:'肌肤之钥光凝前霜',
							createTime:'2021-09-01 19:22:03',
							clockTime:'2021-09-01 19:22:03',
							payTime:'2021-09-01 19:22:03',
							imageSrc:'../../static/logo.png',
							payMoney:99
						}]
					},
					{
						shopName:'会员购北京',
						shopList:[{
							name:'肌肤之钥光凝前霜',
							createTime:'2021-09-01 19:22:03',
							clockTime:'2021-09-01 19:22:03',
							payTime:'2021-09-01 19:22:03',
							imageSrc:'../../static/logo.png',
							payMoney:99
						},]
					},
				] //数据格式
			};
		},
		methods:{
			tabSelect(e){
				this.TabCur = e.currentTarget.dataset.id
			},
			lower1(){
				// 加载更多
			}
		}
	}
</script>

<style lang="scss">
.page{
	.flex{
		display: flex;
	}
	.card{
		background: #fff;
		margin: 40upx 40upx 0 40upx;
		border-radius: 4px;
		image{
			height: 200upx;
			width: 400upx;
		}
		>view{
			padding: 20upx;
		}
		.border-title{
			border-bottom: 1upx solid #ccc;
		}
		.cardItem:not(:last-child) { 
		    border-bottom: 1upx solid #ccc;
		}
	}
}
</style>
