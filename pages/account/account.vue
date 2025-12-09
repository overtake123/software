<template>
	<view class="page">
		<view>
			<u-row customStyle="padding-top: 60rpx; padding-bottom: 80rpx; backgroundColor: #007aff">
			    <u-col span="2" offset="1">
			        <view>
			            <u-avatar size="50" :src="src"></u-avatar>
			        </view>
			    </u-col>
			    <u-col span="8">
			        <view>
			            <u--text color="#ffffff" size="18" mode="name" text="张凯炫" format="encrypt"></u--text>
						<u--text color="#ffffff" size="18" mode="text" text="dianjian001"></u--text>
			        </view>
			    </u-col>
			</u-row>
		</view>
		<view style="margin: -28rpx 40rpx 30rpx">
		    <u-grid
		            :border="true"
		            col="2"
					customStyle="border-radius: 10rpx; backgroundColor: #ffffff"
		    >
		        <u-grid-item>
		            <u--text margin="20rpx 0 10rpx" align="center" size="14" color="#909399" text="部门"></u--text>
		            <u--text margin="0 0 20rpx" align="center" text="检修部"></u--text>
		        </u-grid-item>
				<u-grid-item>
				    <u--text margin="20rpx 0 10rpx" align="center" size="14" color="#909399" text="职务"></u--text>
				    <u--text margin="0 0 20rpx" align="center" text="点检员"></u--text>
				</u-grid-item>
		    </u-grid>
		</view>
		<view class="u-page">
		    <u-list>
				<u-list-item>
					<u-cell
						size="large"
						icon="phone"
						title="电话信息"
						value="13726546542"
				  	></u-cell>
				</u-list-item>
				<u-list-item>
					<u-cell
						size="large"
						icon="lock"
						title="修改密码"
						isLink
						url=""
		        	></u-cell>
				</u-list-item>
				<u-list-item>
					<u-button 
						customStyle="margin-top: 20rpx"
						type="primary"
						plain="true"
						iconColor="#f4f4f5"
						size="large"
						@click="logout()"
						text="退出登录"></u-button>
				</u-list-item>
		    </u-list>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			    src: "/static/avatar.png",
			};
		},
		methods: {
			logout(){
				uni.navigateTo({
				  url: "/pages/login/login"
				});
			}
		}
	}
</script>

<style lang="less">
	
	.page {
		height: 100vh;
		background: #f4f4f5;
	}
	
	.u-page{
		padding:10rpx 24rpx;
	}
	
	.top-fixed{
		position: fixed;
		width: 100%;
		top: 0px;
		margin: 0 0 10rpx 0;
	}
	
	
</style>
