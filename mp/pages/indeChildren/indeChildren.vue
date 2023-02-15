<template>
	<view>
		首页子集页面
		<u-button type="warning" size="medium" @click="go()">点击跳转</u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			go(){
				// 此时会出现顶部返回按键 点击直接返回index页面
				uni.redirectTo({
					url: '/pages/gameChildren/gameChildren?id=1&name=uniapp'
				});
			}
		}
	}
</script>

<style>

</style>
