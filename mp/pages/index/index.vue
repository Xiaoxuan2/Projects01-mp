<template>
	<view class="content">
		
		<image class="logo" src="/static/logo.png" @click="go"></image>
		<view class="text-area">
			<!-- 双花括号渲染 -->
			<text class="title">{{title}}</text>
		</view>
		<!-- 列表渲染 -->
		<view v-for="item in arrylist">
			<p>
				{{item}}
			</p>
		</view>
		<!-- 条件渲染 -->
		<view class="red">
			<view v-if="isOnline">在线{{isOnline}}</view>
			<view v-else>不在线{{isOnline}}</view>
		</view>
		<!-- 三元运算符渲染 -->
		<!-- 如果isFlag未true 类名为redcolor 否则为bluecolor -->
		<view :class="[isFlag?red:blue]">
			三元运算符{{isFlag}}
		</view>
		<!-- 如果number未true 回显1 否则为2 -->
		<view>
			三元运算符{{number?one:two}}
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello微信小程序',
				name: 'names',
				arrylist: ['小明', '小红', '小白'],
				isOnline: false,
				isFlag: false,
				red: 'redcolor',
				blue: 'bluecolor',
				number:true,
				one:"1",
				two:"2",
			}
		},
		onLoad() {
			this.call()
		},
		methods: {
			go() {
				uni.navigateTo({
					url: "/pages/indeChildren/indeChildren"
				})
			},
			// async 异步
			async call(){
					// 导入云对象
					const col1 = uniCloud.importObject('col1')
					//  await 异步 调用say方法
					let res =await col1.say()
					this.con1Text=res.data
					// uni弹窗显示调用的对象
					// uni.showModal({
					// 	content:JSON.stringify(res)
					// })
				}
		}
	}
</script>

<style>
	.redcolor {
		color: red;
	}

	.bluecolor {
		color: blue;
	}

	.isFlag {
		color: antiquewhite;
	}

	.red {
		color: red;
	}

	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
