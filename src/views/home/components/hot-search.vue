<template>
	<div class="hot-search">
		<div class="hot-search__header">
			<span>线上热门搜索</span>
		</div>

		<div class="hot-search__container">
			<el-row class="hot-search__chart" :gutter="100">
				<el-col :md="12" :xs="24">
					<div class="block">
						<div class="count">
							<div class="number">
								<span>搜索用户数</span>
								<span>1242</span>
							</div>
							<div class="rise">
								<i class="el-icon-top-right"></i>
								<span>+7%</span>
							</div>
						</div>

						<v-chart :option="chartOption" autoresize />
					</div>
				</el-col>

				<el-col :md="12" :xs="24">
					<div class="block">
						<div class="count">
							<div class="number">
								<span>搜索用户数</span>
								<span>1242</span>
							</div>
							<div class="rise">
								<i class="el-icon-top-right"></i>
								<span>+7%</span>
							</div>
						</div>

						<v-chart :option="chartOption" autoresize />
					</div>
				</el-col>
			</el-row>

			<div class="hot-search__table">
				<cl-crud @load="onLoad">
					<el-row>
						<cl-table
							:auto-height="false"
							:props="{
								border: false,
								'default-sort': {
									prop: 'ud',
									order: 'descending'
								}
							}"
							:context-menu="false"
							:columns="[
								{
									label: '排名',
									prop: 'index',
									width: 60
								},
								{
									label: '搜索关键词',
									prop: 'keyWord',
									'min-width': 100
								},
								{
									label: '用户数',
									prop: 'users',
									'min-width': 100
								},
								{
									label: '周涨幅',
									prop: 'ud',
									sortable: 'custom',
									'min-width': 100
								}
							]"
						/>
					</el-row>
				</cl-crud>
			</div>
		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";
import * as echarts from "echarts";

export default defineComponent({
	setup() {
		const chartOption = reactive({
			grid: {
				left: 0,
				top: 0,
				right: 0,
				bottom: 0
			},
			xAxis: {
				type: "category",
				data: [
					"00:00",
					"2:00",
					"4:00",
					"6:00",
					"8:00",
					"10:00",
					"12:00",
					"14:00",
					"16:00",
					"18:00",
					"20:00",
					"22:00"
				],
				boundaryGap: false
			},
			yAxis: {
				type: "value",
				splitLine: {
					show: false
				},
				axisTick: {
					show: false
				},
				axisLine: {
					show: false
				},
				axisLabel: {
					show: false
				}
			},
			series: [
				{
					name: "总访问量",
					type: "line",
					smooth: true,
					showSymbol: false,
					symbol: "circle",
					symbolSize: 6,
					data: [
						"1200",
						"1400",
						"1008",
						"1411",
						"1026",
						"1288",
						"1300",
						"800",
						"1100",
						"1000",
						"1118",
						"1322"
					],
					areaStyle: {
						//normal: {
						color: new echarts.graphic.LinearGradient(
							0,
							0,
							0,
							1,
							[
								{
									offset: 0,
									color: "#D1E5FF"
								},
								{
									offset: 1,
									color: "#FFFFFF"
								}
							],
							false
						)
						//}
					},
					itemStyle: {
						//normal: {
						color: "#4165d7"
						//}
					},
					lineStyle: {
						//normal: {
						width: 2
						//}
					}
				}
			]
		});

		function onLoad({ ctx, app }: any) {
			ctx.service({
				page() {
					return Promise.resolve({
						list: [
							{
								index: 1,
								keyWord: "无线耳机",
								users: 983,
								ud: 5
							},
							{
								index: 1,
								keyWord: "运动耳机",
								users: 763,
								ud: -3
							},
							{
								index: 1,
								keyWord: "蓝牙音箱",
								users: 328,
								ud: 7
							},
							{
								index: 1,
								keyWord: "4k显示屏",
								users: 144,
								ud: 4
							},
							{
								index: 1,
								keyWord: "罗技 G530",
								users: 121,
								ud: -1
							}
						]
					});
				}
			}).done();
			app.refresh();
		}

		return { chartOption, onLoad };
	}
});
</script>

<style lang="scss">
.hot-search {
	&__header {
		display: flex;
		align-items: center;
		height: 50px;
		font-size: 15px;
		font-weight: bold;
		padding: 0 20px;
	}

	&__chart {
		padding: 0 20px;

		.block {
			margin: 10px 0;

			.count {
				display: flex;
				align-items: center;
				justify-content: space-between;
				margin-bottom: 10px;
				height: 40px;

				.fall,
				.rise {
					display: flex;
					align-items: center;
					margin-left: 10px;
					font-size: 15px;
				}

				.fall {
					color: #13ae7c;
				}

				.rise {
					color: #f21e37;
				}

				.number {
					display: flex;
					align-items: center;

					span {
						font-size: 13px;

						&:last-child {
							margin-left: 10px;
							font-size: 15px;
							font-weight: bold;
						}
					}
				}
			}

			.echarts {
				height: 50px;
				width: 100%;
			}
		}
	}

	&__table {
		padding: 10px;

		.el-table {
			&__header {
				th {
					background-color: #fff !important;
				}
			}
		}
	}
}
</style>
