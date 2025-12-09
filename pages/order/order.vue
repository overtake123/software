<template>	
	<view>
    <!-- 头部选项卡 -->
		<view class="head-nav">
				<view :class="navIndex==1?'activite':''" @click="checkIndex(1)">待处理</view>
				<view :class="navIndex==2?'activite':''" @click="checkIndex(2)">已处理</view>
				<view :class="navIndex==3?'activite':''" @click="checkIndex(3)">我发布的</view>
		</view>
		<!-- 内容切换 -->
		<view class="content" v-if="navIndex==1">
			<u-cell-group class="order-content" customStyle="padding-bottom: 18rpx" v-for="(item, index) in pendingOrders" :key="item.id">
			    <u-cell 
					isLink
					customStyle="background: #ffffff"
					:title="'巡检点：' + item.name"
					@click="goPage(item.path)"
				>
			    	<view
			    	    slot="value"
			    	    class="u-slot-value"
			    	>
			    		<u-tag
			    		    text="待处理"
			    		    plain
			    		    size="mini"
			    		    type="warning"
			    		>
			    		</u-tag>
			    	</view>
			    </u-cell>
			    <u-cell customStyle="background: #ffffff">
			    	<view
			    	    slot="title"
			    	    class="u-slot-title"
			    	>
						<!-- u-text以时间戳格式读取 -->
			    		<text class="u-cell-text">创建时间：{{ item.time }}</text>
			    	</view>
			    </u-cell>
			</u-cell-group>
			<u-toast ref="uToast" />
		</view>
		<view class="content" v-if="navIndex==2">
			<u-cell-group class="order-content" customStyle="padding-bottom: 18rpx" v-for="(item, index) in completedOrders" :key="item.id">
			    <u-cell 
					isLink
					customStyle="background: #ffffff"
					:title="'巡检点：' + item.name"
					@click="goPage(item.path)"
				>
			    	<view
			    	    slot="value"
			    	    class="u-slot-value"
			    	>
			    		<u-tag
			    		    text="已处理"
			    		    plain
			    		    size="mini"
			    		    type="success"
			    		>
			    		</u-tag>
			    	</view>
			    </u-cell>
			    <u-cell customStyle="background: #ffffff">
			    	<view
			    	    slot="title"
			    	    class="u-slot-title"
			    	>
			    		<text class="u-cell-text">创建时间：{{ item.time }}</text>
			    	</view>
			    </u-cell>
			</u-cell-group>
			<u-toast ref="uToast" />
		</view>
		<view class="content" v-if="navIndex==3">
			<u-cell-group class="order-content" customStyle="padding-bottom: 18rpx" v-for="(item, index) in publishedOrders" :key="item.id">
			    <u-cell 
					isLink
					customStyle="background: #ffffff"
					:title="'巡检点：' + item.name"
					@click="goPage(item.path)"
				>
			    	<view
			    	    slot="value"
			    	    class="u-slot-value"
			    	>
			    		<u-tag
			    		    text="待分配"
			    		    plain
			    		    size="mini"
			    		>
			    		</u-tag>
			    	</view>
			    </u-cell>
			    <u-cell customStyle="background: #ffffff">
			    	<view
			    	    slot="title"
			    	    class="u-slot-title"
			    	>
			    		<text class="u-cell-text">创建时间：{{ item.time }}</text>
			    	</view>
			    </u-cell>
			</u-cell-group>
			<u-toast ref="uToast" />
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				navIndex:1,
				listIndex:0,
				pendingOrders: [
					{
						id: 1,
						name: '501减速机',
						time: '2025/11/10 09:15:38',
						path: '/pages/orderPending/orderPending'
					},
					{
						id: 2,
						name: '601激光防碰撞',
						time: '2025/11/19 10:09:10'
					}
				],
				completedOrders: [
					{
						id: 1,
						name: '103锚钩',
						time: '2025/11/18 16:31:05',
						path: '/pages/orderCompleted/orderCompleted'
					},
					{
						id: 2,
						name: '501卷扬极限',
						time: '2025/11/18 18:09:16'
					}
				],
				publishedOrders: [
					{
						id: 1,
						name: '801小车端子箱',
						time: '2025/11/18 8:31:05',
						path: '/pages/orderPublished/orderPublished'
					},
					{
						id: 1,
						name: '603大车轮',
						time: '2025/11/19 8:25:38'
					},
					{
						id: 3,
						name: '502大车轮',
						time: '2025/11/19 8:09:47'
					},
					{
						id: 1,
						name: '401抱闸',
						time: '2025/11/20 12:31:25'
					},
					{
						id: 4,
						name: '460 8跨轨道',
						time: '2025/11/20 10:09:16'
					}
				]
			}
		},
		methods:{
			checkIndex(index){
				this.navIndex =index;
			},
			checkListIndex(index){
				this.listIndex=index;
			},
			goPage(path) {
			    if (path) {
			        uni.navigateTo({
			          url: path
			        });
			    } else {
			        this.$refs.uToast.show({
			          message: '未找到此工单，请刷新！',
			          type: 'warning'
			        });
			      }
			}
		}
	}
</script>

<style lang="less">
	
	.head-nav{
		width: 80%;
		margin:20rpx auto;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	
	.activite{
		font-weight: bold;
		border-bottom: 6rpx solid #0065d9;
	}
	
	.head-nav>view{
		padding-bottom: 10rpx;
	}
	
	.box{background: #008000;}
	
	.content{
		height: 100vh;
		background: #f4f4f5;
		padding:10rpx 24rpx;
	}
		
</style>
