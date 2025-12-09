<template>
	<view>
		<!-- 顶端固定搜索栏 -->
		<view class="top-fixed">
			<view style="margin: 16rpx 0 16rpx 16rpx;">
				<u--text bold="true" size="22" text="选择巡检设备"></u--text>
			</view>
			<!-- vue2 - 031 -->
			<u-search placeholder="搜索" v-model="keyword"></u-search>
			<u-line margin="10rpx 0 0 0" color="#2979ff"></u-line>
		</view>
		<!-- 索引列表 -->
		<view class="index-list" style="margin-top: 180rpx;">
			<u-index-list :index-list="indexList" custom-nav-height="100">
				<template v-for="(item, index) in itemArr">
					<u-index-item>
						<u-index-anchor :text="indexList[index]"></u-index-anchor>
						<view class="list-cell" v-for="cell in item">
							<u-cell-group border="false">
								<u-cell
								    :title="cell"
									border="false"
								    isLink
									rightIcon=" "
								    url="/pages/inspection/inspection"
								></u-cell>
							</u-cell-group>
						</view>
					</u-index-item>
				</template>
			</u-index-list>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				keyword: '',
				indexList: ["A", "B", "C", "D", "E"],
				itemArr: [
					['设备A_1','A_2','A_3','A_4'],
					['B_1','B_2','B_3','B_4'],
					['C_1','C_2','C_3','C_4'],
					['D_1','D_2','D_3','D_4'],
					['E_1','E_2','E_3','E_4']
				]
			};
		}
	}
</script>

<style lang="less" scoped>
	
	.top-fixed{
		position: fixed;
		width: 100%;
		top: 0px;
		margin: 0 0 10rpx 0;
	}
	
	.list-cell {
			display: flex;
			box-sizing: border-box;
			width: 92%;
			overflow: hidden;
			color: #323233;
			font-size: 28rpx;
			line-height: 48rpx;
			background-color: #fff;
	}
	
</style>
