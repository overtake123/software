<template>
  <view class="container">

    <!-- 区域选择 -->
    <u-picker
      :show="showPicker"
      :columns="[areaList]"
      keyName="label"
      @confirm="onAreaConfirm"
      @cancel="showPicker = false"
    ></u-picker>

    <u-cell
      title="请选择区域"
      :value="selectedArea || '请选择区域'"
      isLink
      @click="showPicker = true"
      :border="false"
    ></u-cell>

    <!-- 问题描述 -->
    <view class="section">
      <view class="label">问题描述</view>
      <u--textarea
        v-model="description"
        placeholder="请输入问题描述信息"
        border="surround"
      ></u--textarea>
    </view>

    <!-- 图片上传 -->
    <view class="section">
      <u-upload
        :fileList="fileList"
        @afterRead="afterRead"
        @delete="onDelete"
        name="1"
        upload-text="上传图片"
        multiple
        :maxCount="3"
      ></u-upload>
    </view>

    <!-- 紧急程度选择 -->
    <view class="section">
      <view class="label">请选择工单紧急程度</view>
      <u-radio-group v-model="urgency">
        <view v-for="item in urgencyList" :key="item.value" class="urgency-option">
          <view class="urgency-tag">{{ item.value }}</view>
          <view class="urgency-label">{{ item.label }}</view>
          <u-radio :name="item.value" />
        </view>
      </u-radio-group>
    </view>

    <!-- 提交按钮 -->
    <view class="submit-btn">
      <u-button type="primary" shape="circle" @click="submitOrder">
        立即创建工单
      </u-button>
    </view>

  </view>
</template>

<script>
export default {
  data() {
    return {
      // 区域选择
      showPicker: false,
      selectedArea: '',
      areaList: [
        { label: '460区域', value: 'area1' },
        { label: '159区域', value: 'area2' },
        { label: '180区域', value: 'area3' }
      ],

      // 问题描述
      description: '',

      // 图片上传
      fileList: [],

      // 紧急程度
      urgency: '',
      urgencyList: [
        { label: '低', value: '1' },
        { label: '中', value: '2' },
        { label: '高', value: '3' },
        { label: '紧急', value: '4' }
      ]
    };
  },
  methods: {
    // 选择区域
    onAreaConfirm(e) {
      this.selectedArea = e.value[0].label;
      this.showPicker = false;
    },
    
    // 上传图片
    afterRead(event) {
      const { file } = event;
      this.fileList.push({ url: file.url });
    },

    onDelete(event) {
      this.fileList.splice(event.index, 1);
    },

    // 提交工单
    submitOrder() {
      if (!this.selectedArea || !this.description || !this.urgency) {
        uni.$u.toast('请完善工单信息');
        return;
      }

      // 模拟提交
      console.log('提交数据：', {
        区域: this.selectedArea,
        描述: this.description,
        紧急程度: this.urgency,
        图片: this.fileList
      });

      uni.$u.toast('工单已提交');
    }
  }
};
</script>

<style scoped>
.container {
  padding: 20rpx;
  background-color: #f5f5f5;
}

.section {
  margin-top: 30rpx;
  background-color: #fff;
  padding: 20rpx;
  border-radius: 10rpx;
}

.label {
  font-weight: bold;
  font-size: 32rpx;
  margin-bottom: 20rpx;
}

.urgency-option {
  display: flex;
  align-items: center;
  margin: 15rpx 0;
}

.urgency-tag {
  width: 50rpx;
  height: 50rpx;
  background-color: #3c9cff;
  color: white;
  text-align: center;
  line-height: 50rpx;
  border-radius: 8rpx;
  margin-right: 20rpx;
}

.urgency-label {
  flex: 1;
  font-size: 30rpx;
}

.submit-btn {
  margin: 60rpx 0;
  padding: 0 30rpx;
}
</style>