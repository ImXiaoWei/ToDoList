<template>
	<div class="content">
		<el-row type="flex" align="middle">
			<!-- 左侧图标 -->
			<el-col :span="3">
				<slot name="start-icon"></slot>
			</el-col>
			<!-- 中部内容 -->
			<el-col :span="18">
				<div class="middle">
					<!-- 标题 -->
					<div class="top-text">
						<slot name="top-text"></slot>
					</div>
					<!-- 时间 -->
					<div class="bottom-text">
						<slot name="bottom-text"></slot>
					</div>
				</div>
			</el-col>
			<!-- 右侧图标 -->
			<el-col :span="3">
				<div class="end-icon"><i class="el-icon-more-outline"></i></div>
			</el-col>
		</el-row>
	</div>
</template>

<script>
	export default {}
</script>

<style>
	.content {
		margin: 20px 0 0 0;
		padding: 10px;
		border-radius: 12px;
		color: #666;
	}

	.end-icon {
		font-size: 25px;
		margin-right: 8px;
	}

	.top-text {
		font-size: 16px;
		font-weight: 400;
		margin-bottom: 5px;
	}

	.bottom-text {
		font-size: 14px;
		font-weight: 400;
		color: steelblue;
	}

	.middle {
		margin-left: 8px;
	}
</style>
