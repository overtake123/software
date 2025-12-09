<template>
  <view class="container">
    <view class="logo-box">
      <image
			src="/static/login.png"
			class="logo"
			mode="aspectFit"
      />
      <view class="title">智能巡检系统</view>
    </view>
    <!-- 表单区域 -->
    <view class="form-box">
      <!-- 用户名输入 -->
		<u-input
			v-model="username"
			placeholder="请输入用户名"
			prefixIcon="account"
			border="bottom"
		></u-input>
		  <!-- 密码输入（自定义右侧图标） -->
		<view class="password-row">
			<u-input
				class="password-input"
				v-model="password"
				placeholder="请输入密码"
				:password="!showPassword"
				prefixIcon="lock"
				border="bottom"
			></u-input>
        <u-icon
			:name="showPassword ? 'eye-off' : 'eye'"
			size="22"
			color="#999"
			@click="togglePassword"
        ></u-icon>
		</view>
    </view>
    <!-- 登录按钮 -->
    <view class="btn-box">
		<u-button
			type="primary"
			shape="circle"
			text="登录"
			@click="login"
		></u-button>
    </view>
    <!-- Toast 提示 -->
    <u-toast ref="uToast" />
  </view>
</template>

<script>
	export default {
		data() {
			return {
				username: '', 
				password: '',
				showPassword: false
			};
		},
		methods: {
			togglePassword() {
				this.showPassword = !this.showPassword;
			},
			login() {
				if (!this.username || !this.password) {
					uni.$u.toast('请输入用户名和密码');
				return;
				}
				// 模拟登录成功
				uni.$u.toast('登录成功');
				// 页面跳转，示例跳转到首页（假设首页是 tabBar 页面）
				setTimeout(() => {
					uni.switchTab({
					  url: '/pages/home/home'
					});
				}, 800); // 延迟跳转，使 toast 有时间显示
			}
		}
};
</script>

<style lang="less">
	.container {
		padding: 60rpx 40rpx;
		background-color: #ffffff;
		min-height: 100vh;
		box-sizing: border-box;
	}
	
	.logo-box {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-top: 120rpx;
		margin-bottom: 100rpx;
	}
	
	.logo {
		width: 150rpx;
		height: 150rpx;
		margin-bottom: 30rpx;
	}
	
	.title {
		font-size: 40rpx;
		font-weight: bold;
		color: #2c3e50;
	}
	
	.form-box {
		margin-bottom: 80rpx;
	}
	
	.btn-box {
		padding: 0 20rpx;
	}
	
	.password-row {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 10rpx 0;
	}
	
	.password-input {
		flex: 1;
		margin-right: 20rpx;
	}	
</style>