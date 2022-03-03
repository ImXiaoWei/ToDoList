<template>
	<div>
		<el-row type="flex" class="row-bg" justify="space-around">
			<el-col>
				<!-- 卡片 -->
				<el-card class="box-card">
					<div class="title"><span class="el-icon-date"> 待 办 事 项 </span></div>
					<!-- 待办事项 -->
					<div class="todo">
						<!-- 无数据时提示 -->
						<div v-show="todoList.length==0">
							<el-result icon="success" title="已完成全部事项">
								<template slot="extra">
									<el-button>新建事项</el-button>
								</template>
							</el-result>
						</div>
						<Lable :class="todoListStyle(item.state)" v-for="(item,index) in todoList" :key="index"
							:activeStyle="todoStyle">
							<template slot="top-text">
								{{item.title}}
							</template>
							<template slot="bottom-text">
								{{item.date}}
							</template>
							<template slot="start-icon">
								<div class="todo-icon">
									<i class="el-icon-full-screen" @click="finished();item.done=true"></i>
								</div>
							</template>
						</Lable>
					</div>
					<!-- 完成事项 -->
					<div class="done" v-show="doneCount>0">
						<div class="complete">
							<el-divider content-position="left"><span id="completeFont"> 已完成 </span>
								<el-tag type="success" size="medium">{{doneCount}}</el-tag>
							</el-divider>
						</div>
						<Lable class="doneListStyle" v-for="(item,index) in doneList" :key="index"
							:activeStyle="doneStyle">
							<template slot="top-text">
								{{item.title}}
							</template>
							<template slot="bottom-text">
								{{item.date}}
							</template>
							<template slot="start-icon">
								<div class="todo-icon"><i class="el-icon-circle-check"></i></div>
							</template>
						</Lable>
					</div>
				</el-card>
			</el-col>
		</el-row>
	</div>
</template>

<script>
	import Lable from './Label.vue'
	export default {
		name: 'Home',
		components: {
			Lable
		},
		data() {
			return {
				/* 列表数据 */
				totalList: [{
					title: "Check game board",
					date: "Today,09:00",
					state: 0, // 重要不紧急
					done: false
				}, {
					title: "Watch a painting video",
					date: "Today",
					state: 1, // 重要紧急
					done: false
				}, {
					title: "Paint at night",
					date: "Today",
					state: 2, // 不重要不紧急
					done: false
				}, {
					title: "Check trello",
					date: "Today",
					state: 3, // 不重要紧急
					done: false
				}, {
					title: "What",
					date: "Today",
					state: 4, // 无标记
					done: false
				}, {
					title: "Done",
					date: "Today",
					state: 1, // 无标记
					done: true
				}],
				doneStyle: "",
				todoStyle: "border:1px dashed orangered"

			}
		},
		methods: {
			/* 列表前图标样式 */
			todoListStyle(val) {
				switch (val) {
					case 0:
						return 'state0'
						break;
					case 1:
						return 'state1'
						break;
					case 2:
						return 'state2'
						break;
					case 3:
						return 'state3'
						break;
					default:
						return 'stateDefault'
				}
			},
			/* 完成目标 */
			finished() {
				this.$message({
					message: '完成~',
					type: 'success',
					duration: 700
				});
			}
		},
		computed: {
			/* 已完成事项数量 */
			doneCount() {
				return this.totalList.filter(u => u.done == true).length
			},
			/* 待办列表 */
			todoList() {
				return this.totalList.filter(u => u.done == false)
			},
			/* 已办列表 */
			doneList() {
				return this.totalList.filter(u => u.done == true)
			}
		}
	}
</script>

<style>
	.title {
		font-size: 25px;
		text-align: center;
		margin: 30px;
	}

	.complete {
		margin: 30px 0 20px 0;
		height: 2px;
		background-color: #ccc;
		border: none;
	}

	#completeFont {
		font-size: 20px;
		font-weight: 400;
		color: #67C23A;
	}

	.todo-icon {
		font-size: 25px;
		margin-left: 8px;
	}

	.done-icon {
		font-size: 25px;
		margin-left: 8px;
		color: #67C23A;
	}

	.doneListStyle {
		border: 1px dashed #67C23A;
		background-color: #F0F9EB;
		color: #67C23A
	}

	.state0 {
		border: 1px dashed #409EFF;
		background-color: #ECF5FF;
		color: #409EFF
	}

	.state1 {
		border: 1px dashed #F56C6C;
		background-color: #FDE2E2;
		color: #F56C6C
	}

	.state2 {
		border: 1px dashed #E6A23C;
		background-color: #FDF6EC;
		color: #E6A23C
	}

	.state3 {
		border: 1px dashed #909399;
		background-color: #F4F4F5;
		color: #909399
	}

	.stateDefault {
		border: 1px dashed #ccc;
	}
</style>
