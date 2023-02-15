<template>
	<view>
		game页面
		<!-- touchstart：手指触摸开始   touchend：手指触摸后-->
		<view class="content" @touchstart="startHandle1" @touchend="touchHandle1">
			父节点
			<!-- 使用 .stop 解决 冒泡事件-->
			<view class="" @touchstart.stop="startHandle" @touchend.stop="touchHandle">
				触屏事件的学习
			</view>
		</view>

		<u-button type="warning" size="medium" @click="go()">点击跳转</u-button>
		<!--open-type默认值: navigate -->
		<navigator url="/pages/gameChildren/gameChildren" >
			<button type="default">跳转到新页面</button>
		</navigator>
		<navigator url="/pages/gameChildren/gameChildren" open-type="redirect" >
			<button type="default">在当前页打开</button>
		</navigator>
		<navigator url="/pages/index/index" open-type="switchTab" >
			<button type="default">跳转tab页面</button>
		</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				msg: "111"
			}
		},
		// 小程序生命周期
		onLoad() {
			console.log("onLoad监听页面加载，一个页面只调用一次")
		},
		onShow() {
			console.log("onShow小程序启动时，或从后台进入前台显示")
		},
		onHide() {
			console.log("onHide小程序隐藏")
		},
		// vue生命周期
		beforeCreate() {
			console.log("beforeCreate组件创建前")
		},
		created() {
			console.log("created组件创建后")
		},
		beforeMount() {
			console.log("beforeMount组件挂在前")
		},
		mounted() {
			console.log("mounted组件挂在后")
		},

		methods: {
			startHandle(event) {
				// event 事件属性
				console.log("手指按下", event);
			},
			touchHandle(event) {
				console.log("手指离开");
			},
			startHandle1(event) {
				console.log("手指按下1");
			},
			touchHandle1(event) {
				console.log("手指离开1");
			},
			go() {
				// 方式一
				// navigateTo跳转至子页面，携带id和name参数
				uni.navigateTo({
					url: "/pages/gameChildren/gameChildren?id=1&name=uniapp"
				})

				// 方式二：redirectTo跳转，（此时已关闭game页面，顶部不会有返回键）
				// uni.redirectTo({
				// 	url: '/pages/gameChildren/gameChildren?id=1&name=uniapp'
				// });

				// 方式三 (注意：此时已关闭所有页面，不会再有顶部返回按键)
				// uni.reLaunch({
				// 	url:"/pages/gameChildren/gameChildren?id=1&name=uniapp"
				// })

				// 方式四  （只能跳转到tabBar页面）
				// uni.switchTab({
				// 	url: '/pages/index/index'
				// });

				// 方式五 navigateBack跳转（见gameChildren页面）


			}
		}
	}
</script>

<style>

</style>
