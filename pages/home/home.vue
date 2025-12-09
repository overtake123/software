<template>
	<view>
		<u-notice-bar 
				:text="notice" 
				mode="link" 
				speed="100" 
				url=""
		></u-notice-bar>
		<!--  -->
		<view class="page">
		<view class="u-message-blockt">
			<view class="u-message-block__content">
				<u-row>
					<u-col>
						<view class="message-title-layout">
							<u--text color="#FFFFFF" text="今日"></u--text>
						</view>
					</u-col>
				</u-row>
				<u-row customStyle="margin-bottom: 5px">
					<u-col span="6">
					    <view class="message-layout" style="border-radius: 0 0 0 20rpx;">
					    	<u--text size="24rpx" align="center" lineHeight="50rpx" margin="10rpx 0 0 0" color="#FFFFFF" text="巡检次数"></u--text>
					    	<u--text size="58rpx" align="center" lineHeight="100rpx" color="#FFFFFF" text="0"></u--text>
					    </view>
					</u-col>
					<u-col span="6">
					    <view class="message-layout" style="border-radius: 0 0 20rpx 0;">
					    	<u--text size="24rpx" align="center" lineHeight="50rpx" margin="10rpx 0 0 0" color="#FFFFFF" text="异常次数"></u--text>
					    	<u--text size="58rpx" align="center" lineHeight="100rpx" color="#FFFFFF" text="0"></u--text>
					    </view>
					</u-col>
				</u-row>
			</view>
		</view>
		<!-- 分栏间隔设置 -->
		<view class="u-block__content">
		    <u-row
		            justify="space-between"
		            gutter="10"
		    >
		        <u-col span="4" textAlign="center">
		            <view>
						<u-button
								type="primary"
								size="large"
								icon="scan"
								color="#30BAA1"
								text="扫码巡检"
						></u-button>
					</view>
		        </u-col>
		        <u-col span="4" textAlign="center">
		            <view>
						<u-button
								type="primary"
								size="large"
								icon="checkbox-mark" 
								color="#456EFE"
								text="手动巡检"
						></u-button>
					</view>
		        </u-col>
		        <u-col span="4" textAlign="center">
		            <view>
						<u-button
								type="primary"
								size="large"
								icon="plus-square-fill" 
								color="#15B9EE"
								@click="createorder()"
								text="创建工单"
						></u-button>
					</view>
		        </u-col>
		    </u-row>
		</view>
		<!-- 底部导航栏；切换菜单之前，进行回调鉴权 -->
		<!-- <u-tabbar :placeholder="true" :value="value3" @change="name => value3 = name" :fixed="true"
			:safeAreaInsetBottom="false">
		</u-tabbar> -->
		<!-- 宫格布局 -->
		<view style="padding: 20rpx;">
		    <u-grid
		            :border="true"
					col="3"
		    >
		        <u-grid-item
						class="icon-layout"
		                v-for="(listItem,listIndex) in list"
		                :key="listIndex"
						@click="goPage(listItem.path)"
		        >
		            <u-icon
		                    :customStyle="{paddingTop:20+'rpx'}"
		                    :name="listItem.name"
		                    :size="28"
		            ></u-icon>
		            <text class="grid-text">{{listItem.title}}</text> 
		        </u-grid-item>
		    </u-grid>
		    <u-toast ref="uToast" />
		</view>
		<!-- 分隔栏设置 -->
		<view class="u-demo-block__content">
		    <u-row
		            justify="space-between"
		            gutter="10"
		    >
		        <u-col span="3" textAlign="center">
		            <view class="warning-text">
		            	<u--text size="50rpx" align="center" lineHeight="90rpx" margin="10rpx 0 0 0" color="#dd6161" text="10"></u--text>
						<u--text size="24rpx" align="center" lineHeight="10rpx" margin="0 0 30rpx 0" color="#909399" text="今日未巡检"></u--text>
		            </view>
		        </u-col>
		        <u-col span="3" textAlign="center">
		            <view class="warning-text">
		            	<u--text size="50rpx" align="center" lineHeight="90rpx" margin="10rpx 0 0 0" color="#dd6161" text="1"></u--text>
		            	<u--text size="24rpx" align="center" lineHeight="10rpx" margin="0 0 30rpx 0" color="#909399" text="本周未巡检"></u--text>
		            </view>
		        </u-col>
		        <u-col span="3" textAlign="center">
		            <view class="warning-text">
		            	<u--text size="50rpx" align="center" lineHeight="90rpx" margin="10rpx 0 0 0" color="#dd6161" text="0"></u--text>
		            	<u--text size="24rpx" align="center" lineHeight="10rpx" margin="0 0 30rpx 0" color="#909399" text="本月未巡检"></u--text>
		            </view>
		        </u-col>
		        <u-col span="3" textAlign="center">
		            <view class="warning-text">
		            	<u--text size="50rpx" align="center" lineHeight="90rpx" margin="10rpx 0 0 0" color="#dd6161" text="0"></u--text>
		            	<u--text size="24rpx" align="center" lineHeight="10rpx" margin="0 0 30rpx 0" color="#909399" text="本季未巡检"></u--text>
		            </view>
		        </u-col>
		    </u-row>
			<u-row
			        justify="space-between"
			        gutter="10"
			>
			    <u-col span="3">
			        <view class="warning-text">
			        	<u--text size="50rpx" align="center" lineHeight="90rpx" margin="10rpx 0 0 0" color="#dd6161" text="0"></u--text>
			        	<u--text size="24rpx" align="center" lineHeight="10rpx" margin="0 0 30rpx 0" color="#909399" text="本年未巡检"></u--text>
			        </view>
			    </u-col>
			</u-row>
		</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				notice: '今日有未完成的巡检任务！',
				list: [{
						name: '/static/setting.png',
						title: '巡检记录',
						path: '/pages/inspectionRecords/inspectionRecords'
				    },
				    {
				        name: '/static/inventory.png',
				        title: '库存分析'
				    },
				    {
				        name: '/static/record.png',
				        title: '巡检点统计'
				    },
				    {
				        name: '/static/record.png',
				        title: '巡检人统计'
				    },
				    {
				        name: 'home',
				        title: '巡检点设置'
				    },
					{
					    name: '',
					    title: ''
					},
				],
			};
		},
		methods: {
		    goPage(path) {
		        if (path) {
		            uni.navigateTo({
		              url: path
		            });
		        } else {
		            this.$refs.uToast.show({
		              message: '功能未开放！',
		              type: 'warning'
		            });
		          }
		    },
			createorder(){
				uni.navigateTo({
				  url: "/pages/orderCreate/orderCreate"
				});
			}
		},
		mounted() {
			console.log(uni.$u.pages());
		}
	}
</script>

<style lang="less">
	
	.page {
		height: 100vh;
		background: #ffffff;
		padding:10rpx 24rpx;
	}
	
	.message-title-layout {
		background-color: #2b85e4;
		height: 40rpx;
		border-radius: 20rpx 20rpx 0 0;
		padding: 20rpx 10rpx;
	}
	
	.message-layout{
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: #2979ff;
		height: 160rpx;
	}
	
	.warning-text{
		background-color: #f4f4f5;
		border-radius: 10rpx;
		height: 140rpx;
	}
	
	.grid-text {
	    font-size: 14px;
		font-weight: bold;
	    color: black;
	    padding: 10rpx 0 20rpx 0rpx;
	    /* #ifndef APP-PLUS */
	    box-sizing: border-box;
	    /* #endif */
	}
</style>