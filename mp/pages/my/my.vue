<template>
	<view>
		<view class="">
			<!-- udb快捷键 获取数据库数据 data：数据  mydata数据表名称-->
			<unicloud-db ref="data" v-slot:default="{data, loading, error, options}" collection="mydata">
				<view v-if="error">{{error.message}}</view>
				<view v-else>
				</view>
			</unicloud-db>
			<!--show:打开或者关闭某个组件  open:组件触发打开状态时 options:左滑按钮 -->	
			<u-swipe-action :show="item.show" :index="index" v-for="(item, index) in list" :key="item._id"
				@click="click" @open="open(index,item)" :options="options">
				<view class="item u-border-bottom" style="line-height: 50px; border-bottom: 1px solid #999;">
					<view class="title-wrap" style="margin-right: 20px;">
						姓名：{{item.name}}
					</view>
					<view class="title-wrap">
						手机号码：{{item.phone}}
					</view>
				</view>
			</u-swipe-action>
		</view>
		<u-modal v-model="modelShow" :content="content" @confirm="comfrim" :show-cancel-button="true">
			<u-field v-model="item.name" label="姓名" placeholder="请填写姓名" :required="true">
			</u-field>
			
			<u-field v-model="item.phone" label="手机号" placeholder="请填写手机号" :required="true">>
			</u-field>
		</u-modal>
		<button @click="add" style="margin-top: 20px;">添加</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content: "新增",
				item: {
					name: "",
					phone: "",
					show: false,
				},
				modelShow: false,
				list:[],
				show: false,
				options: [{
						text: '修改',
						style: {
							backgroundColor: '#007aff'
						}
					},
					{
						text: '删除',
						style: {
							backgroundColor: '#dd524d'
						}
					}
				],
				type:'',
				_id:''
			};
		},
		mounted() {
			// 用ref拿到数据库中的dataList值赋值给到list
			console.log(this.$refs.data)
			this.list = this.$refs.data.$data.dataList
		},
		methods: {
			// 左滑点击事件
			click(index,index1) {
				console.log(index,index1)
				// index1==1为删除
				if (index1 == 1) {
					this.$refs.data.remove(this.list[index]._id)
				// 否则为修改
				} else {
					this.type=2;
					// 将拿到的this.list[index]数据赋值给到item用于修改模态框回显
					this.item=this.list[index]
					// 将拿到的数据id值赋值给this._id用于修改时上传
					this._id=this.list[index]._id
					this.modelShow = true;
					this.list[index].show = false;
				}
			},
			// 按钮添加事件
			add() {
				// 显示模态框
				this.modelShow = true
				this.type=1
			},
			// 模态框确认事件
			comfrim() {
				// 调用uniCloud数据库
				const db = uniCloud.database();
				// type为1时为 添加事件 
				if (this.type == 1) {
					// 使用 mydata 云数据表  使用 add添加函数
					db.collection('mydata').add(this.item).then(e => {
						this.$u.toast("新增成功");
						// 清空模态框数据
						this.item = {
							name: "",
							phone: "",
							show: false
						}
						// 使用refresh函数清空并重新加载当前页面数据
						this.$refs.data.refresh()
						// 重新将数据赋值
						this.list = this.$refs.data.$data.dataList
					})
				// type为2时为 修改事件 
				} else if (this.type == 2) {
					// 使用 mydata 云数据表  使用doc传递修改id、使用update修改函数
					delete this.item._id
					console.log(this.list)
					db.collection('mydata').doc(this._id).update(this.item).then(e => {
						
						this.$u.toast("修改成功");
						this.item = {
							name: "",
							phone: "",
							show: false
						}
					})
				}
			},
			// 左滑事件
			open(index,item) {
				this.list[index].show = true;
			}
			
		}
	}
</script>

<style lang="scss" scoped>
	.item {
		display: flex;
		padding: 20rpx;
	}

	image {
		width: 120rpx;
		flex: 0 0 120rpx;
		height: 120rpx;
		margin-right: 20rpx;
		border-radius: 12rpx;
	}

	.title {
		text-align: left;
		font-size: 28rpx;
		color: $u-content-color;
		margin-top: 20rpx;
	}
</style>
