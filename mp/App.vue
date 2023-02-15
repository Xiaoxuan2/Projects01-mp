<script>
	export default {
		onLaunch: function() {
			console.log('App Launch小程序初始化完成时')
		},
		onShow: function() {
			console.log('App Show小程序启动时')
		},
		onHide: function() {
			console.log('App Hide')
		},
		onError:function(){
			console.log('APP Error')
		}
	}
</script>
<!-- 每个公共页面的css -->
<style lang="scss">
	/* 注意要写在第一行，同时给style标签加入lang="scss"属性 */
	@import "uview-ui/index.scss";
</style>
