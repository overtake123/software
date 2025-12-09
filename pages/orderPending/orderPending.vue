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
      <input
        class="repair-input"
        placeholder="请输入维修说明"
        v-model="repairDesc"
      />
      <view class="upload-box" @click="chooseImage">
        <view class="upload-btn">
          <text class="plus">+</text>
          <text class="upload-text">上传图片</text>
        </view>
        <image
          v-if="repairImage"
          :src="repairImage"
          class="preview-image"
          mode="aspectFit"
        />
      </view>
    </view>

    <!-- 提交按钮 -->
    <view class="footer">
      <button class="submit-btn" @click="submit">立即提交</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      pointName: '501减速机',
      problemDesc: '减速机更换',
      problemImage: '/static/jiansuji.jpg', // 示例图路径，自行替换
      repairDesc: '',
      repairImage: ''
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

.upload-box {
  border: 1rpx dashed #ccc;
  width: 200rpx;
  height: 200rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8rpx;
  position: relative;
}

.upload-btn {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.plus {
  font-size: 48rpx;
  color: #999;
}

.upload-text {
  font-size: 24rpx;
  color: #999;
}

.preview-image {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 8rpx;
  object-fit: cover;
}

.footer {
  margin-top: 60rpx;
  padding: 0 40rpx;
}

.submit-btn {
  background-color: #3c8cff;
  color: #fff;
  font-size: 30rpx;
  border-radius: 50rpx;
  height: 90rpx;
  line-height: 90rpx;
}
</style>