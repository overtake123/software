<template>
	<view>
		<u-action-sheet :actions="list" :title="title" :show="show"></u-action-sheet>
		<u-button @click="show = true">打开ActionSheet</u-button>
		
		<u-button @click="router1">测试</u-button>
		<u-search placeholder="日照香炉生紫烟" v-model="keyword"></u-search>
		去除所有空格：{{$u.trim(str, 'all')}}
	</view>
</template>

<script>
import homeVue from '../home/home.vue';

	export default {
		data() {
			return {
				str: 'a  b c ',
				keyword: '遥看瀑布挂前川',
				title: '标题',
				list: [{
						name: '选项一',
						subname: "选项一描述",
						color: '#ffaa7f',
						fontSize: '20'
					},
					{
						name: '选项二禁用',
						disabled: true
					},
					{
						name: '开启load加载', //开启后文字不显示
						loading: true
					}
				],
				show: false
			};
		},
		methods: {
			router1(){
				uni.navigateTo({
					url:"/pages/device1/device1"
				})
			}
			
			
		},
	};
</script>