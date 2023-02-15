<template>
	<view>
		子页面
		<p>
			携带的参数：{{options.name}}
		</p>
		<u-button type="warning" size="medium" @click="go()">点击跳转</u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				options: ''
			}
		},
		methods: {
			go() {
				// 
				uni.navigateBack({
					delta: 1
				});

			}
		},
		// 接受game页面传递的参数
		onLoad(options) {
			this.options = options
			console.log(options)
		}
	}
</script>

<style>

</style>
