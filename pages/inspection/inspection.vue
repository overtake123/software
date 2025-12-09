<template>
	<view class="page">
		<!-- 注意，如果需要兼容微信小程序，最好通过setRules方法设置rules规则 -->
		<u--form
				labelPosition="left"
				:labelStyle='lstyle'
				:model="model1"
				:rules="rules"
				ref="uForm"
		>
			<u-form-item
					label="设备名称"
					labelWidth="100"
					labelPosition="top" 
					borderBottom
					ref="deviceName"
			>
				<u--text bold="true" size="25" text="设备A_1"></u--text>
			</u-form-item>
			
			<u-form-item
					v-for="(item, id) in inspectionitems"
					:key="id"
					:prop="'inspectionitems[' + id + '].item'"
					:label="item.id + '. ' + item.item"
					labelWidth="375"
					labelPosition="top" 
					borderBottom
					@click="showSex = true; hideKeyboard()"
					ref="deviceItems"
			>
			<u-radio-group 
			    v-model="value"
			    placement="row">
				<u-radio customStyle="margin: 20rpx 50rpx 0 20rpx" activeColor="#1463FD" label="正常"></u-radio>
				<u-radio customStyle="margin: 20rpx 50rpx 0 20rpx" activeColor="#fa3534" label="异常"></u-radio>
			</u-radio-group>	
			</u-form-item>
			
			<u-form-item
					required="true"
					label="上传巡检图片"
					labelWidth="150"
					labelPosition="top" 
					borderBottom
					ref="deviceName"
			>
				<u-upload
				  :fileList="fileList2"
				  @afterRead="afterRead"
				  @delete="deletePic"
				  name="2"
				  :maxCount="10"
				  capture="camera"
				></u-upload>
			</u-form-item>
			
			<u-form-item
					label="上报设备状态为"
					labelWidth="150"
					labelPosition="top" 
					prop="device.name"
					borderBottom
					ref="deviceStatus"
			>
				<u-radio-group 
				    v-model="value"
					shape="square"
					iconPlacement="right">
					<u-radio customStyle="margin: 20rpx 50rpx 0 20rpx" activeColor="#1463FD" label="正常" labelSize="46rpx" size="46rpx"></u-radio>
					<u-radio customStyle="margin: 20rpx 50rpx 0 20rpx" activeColor="#fa3534" label="异常" labelSize="46rpx" size="46rpx"></u-radio>
				</u-radio-group>
			</u-form-item>
			
			<u-form-item
					label="备注"
					labelWidth="150"
					labelPosition="top" 
					prop="remark"
					borderBottom
					ref="remark"
			>
				<u--textarea v-model="value1" placeholder="请输入巡检备注" ></u--textarea>
			</u-form-item>
		</u--form>
		<u-toast ref="uToast"></u-toast>
		<u-button 
				customStyle="margin-top: 20rpx;"
				shape="circle"
				color="linear-gradient(to right, rgb(47, 170, 255), rgb(40, 134, 186))"
				text="提交"
				@click="submit(success)">
		</u-button>
	</view>
</template>

<script>
export default {
	data() {
		return {
			showSex: false,
			inspectionitems: [{
				id: '001',
				item: '电机运转平稳，地脚螺栓紧固不松动',
				},
				{
					id: '002',
					item: '风机运转平稳，无异响',
				},
				{
					id: '003',
					item: '电机周围是否有异味',
				},
				{
					id: '004',
					item: '电缆管完好，电机附近无火灾隐患',
				},
			],
			success: {
				type: "success",
				title: "成功主题(带图标)",
				message: "提交成功",
				iconUrl: "https://uviewui.com/demo/toast/success.png",
			},
			rules: {
				'userInfo.name': {
					type: 'string',
					required: true,
					message: '请填写姓名',
					trigger: ['blur', 'change']
				},
				'userInfo.sex': {
					type: 'string',
					max: 1,
					required: true,
					message: '请选择男或女',
					trigger: ['blur', 'change']
				},
			},
			value1: '',
			radio: '',
			switchVal: false,
			fileList2: [],
		};
	},
	methods: {
		submit(params) {
		        this.$refs.uToast.show({
		          ...params,
		          complete() {
		            params.url &&
		              uni.navigateTo({
		                url: params.url,
		              });
		          },
		        });
		      },
	      // 删除图片
	      deletePic(event) {
	        this[`fileList${event.name}`].splice(event.index, 1);
	      },
	      // 新增图片
	      async afterRead(event) {
	        // 当设置 multiple 为 true 时, file 为数组格式，否则为对象格式
	        let lists = [].concat(event.file);
	        let fileListLen = this[`fileList${event.name}`].length;
	        lists.map((item) => {
	          this[`fileList${event.name}`].push({
	            ...item,
	            // status: "uploading",
	            // message: "上传中",
	          });
	        });
	        for (let i = 0; i < lists.length; i++) {
	          const result = await this.uploadFilePromise(lists[i].url);
	          let item = this[`fileList${event.name}`][fileListLen];
	          this[`fileList${event.name}`].splice(
	            fileListLen,
	            1,
	            Object.assign(item, {
	              status: "success",
	              message: "",
	              url: result,
	            })
	          );
	          fileListLen++;
	        }
	      },
	      uploadFilePromise(url) {
	        return new Promise((resolve, reject) => {
	          let a = uni.uploadFile({
	            url: "http://192.168.2.21:7001/upload", // 仅为示例，非真实的接口地址
	            filePath: url,
	            name: "file",
	            formData: {
	              user: "test",
	            },
	            success: (res) => {
	              setTimeout(() => {
	                resolve(res.data.data);
	              }, 1000);
	            },
	          });
	        });
	      },
	    },
	computed: {
	    lstyle() {
	      return {
	        color: '#303133',
			fontSize: '34rpx'
	      };
	    }
	  },
};
</script>

<style lang="less">
	
	.page {
		height: 100vh;
		background: #ffffff;
		padding:10rpx 24rpx;
	}
	
	.labelstyle{
		color: "#909399";
	}
	
</style>
