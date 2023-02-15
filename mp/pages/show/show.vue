<template>
	<view>
		演出页面
		<u-button type="warning">警告按钮</u-button>

		<view v-for="item in MsgData">
			{{item.catalog}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				MsgData: {}
			}
		},
		methods: {
				http(){
					uni.request({
						// 请求路径
						url: 'http://apis.juhe.cn/goodbook/catalog',
						//参数
						data: { 
							dtype: "",
							key:"adc55f56b297791c849efd1162039e8d"
						},
						//请求方式  或GET，必须为大写
						method: 'GET', 
						success: res => {
							console.log('成功', res.data);
							this.MsgData = res.data.result
						},
						fail: (err) => {
							console.log('失败', res.data);
						}
					})
				}
		},
		onShow() {
			this.http()
		}
	}
</script>

<style>

</style>
