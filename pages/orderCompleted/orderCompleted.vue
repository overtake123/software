<template>
  <view class="container">
    <!-- 巡检点显示 -->
    <view class="card">
      <view class="label">巡检点：<text class="value">{{ pointName }}</text></view>
    </view>

    <!-- 问题描述 -->
    <view class="card">
      <view class="section-title">问题描述</view>
      <view class="text-content">{{ problemDesc }}</view>
      <image
        class="problem-image"
        :src="problemImage"
        mode="aspectFit"
      />
    </view>

    <!-- 维修说明 -->
    <view class="card">
      <view class="section-title">维修说明</view>
	  <view class="text-content">{{ repairDesc }}</view>
	  <image
	    class="problem-image"
	    :src="repairImage"
	    mode="aspectFit"
	  />
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      pointName: '103锚钩',
      problemDesc: '更换锚钩',
      problemImage: '/static/huaimaogou.jpg', // 示例图路径，自行替换
      repairDesc: '460分厂一跨103吊车更换锚钩一个西侧',
      repairImage: '/static/maogou.jpg'
    };
  },
  methods: {
    chooseImage() {
      const that = this;
      wx.chooseImage({
        count: 1,
        success(res) {
          that.repairImage = res.tempFilePaths[0];
        }
      });
    },
    submit() {
      if (!this.repairDesc) {
        wx.showToast({
          title: '请输入维修说明',
          icon: 'none'
        });
        return;
      }

      wx.showToast({
        title: '提交成功',
        icon: 'success'
      });

      // 可在此发起网络请求提交数据
    }
  }
};
</script>

<style scoped>
.container {
  background-color: #f5f5f5;
  padding: 20rpx;
  min-height: 100vh;
  box-sizing: border-box;
}

.card {
  background-color: #fff;
  margin-bottom: 20rpx;
  padding: 24rpx;
  border-radius: 12rpx;
}

.label {
  font-size: 30rpx;
  color: #333;
}

.value {
  font-weight: bold;
}

.section-title {
  font-size: 28rpx;
  font-weight: bold;
  margin-bottom: 16rpx;
  color: #333;
}

.text-content {
  font-size: 26rpx;
  color: #666;
  margin-bottom: 16rpx;
}

.problem-image {
  width: 200rpx;
  height: 200rpx;
  border-radius: 8rpx;
}

.repair-input {
  border: 1rpx solid #ccc;
  border-radius: 8rpx;
  padding: 16rpx;
  font-size: 26rpx;
  margin-bottom: 20rpx;
}

</style>