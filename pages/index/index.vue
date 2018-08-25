<template>
	<view class="page-body">
		<view class="page-section">
			<text class="title">{{title}}</text>
			<button type="primary" @tap="loadoption">Click Me!</button>
		</view>
		<view class="page-section">
			<view>图表一（线图）</view>
			<view class="chart">
				<myChart :option="optionOne" canvasId="chartOne" />
			</view>
		</view>
		<view class="page-section">
			<view>图表二（柱状图）</view>
			<view class="chart">
				<myChart :option="optionTwo" canvasId="chartTwo" />
			</view>
		</view>
	</view>
</template>

<script>
	import myChart from '../../components/myChart.vue'
	
	export default {
		components: {
			myChart
		},
		data() {
			return{
				title: 'Hello',
				// 第一个chart的option 线图
				optionOne:  {
					title: {
						text: 'ECharts 入门示例'
					},
					tooltip: {},
					legend: {
						data:['销量']
					},
					xAxis: {
						data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
					},
					yAxis: {},
					series: [{
						name: '销量',
						type: 'line',
						data: [5, 20, 36, 10, 10, 20]
					}]
				},
				// 第二个chart的option 柱状图
				optionTwo:  {
					title: {
						text: 'ECharts 入门示例'
					},
					tooltip: {},
					legend: {
						data:['销量']
					},
					xAxis: {
						data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
					},
					yAxis: {},
					series: [{
						name: '销量',
						type: 'bar',
						data: [5, 20, 36, 10, 10, 20]
					}]
				},
				// 连续点击按钮用的flag
				flag: true
			}
		},
		methods: {
			// 点击一次
			loadoption(){
				// 点击单数次加载这里的option 数值从高到低
				if (this.flag === true) {
					this.flag = false
					this.optionOne = {
						title: {
							text: 'ECharts 入门示例'
						},
						tooltip: {},
						legend: {
							data:['销量']
						},
						xAxis: {
							data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
						},
						yAxis: {},
						series: [{
							name: '销量',
							type: 'line',
							data: [50, 40, 36, 20, 10, 0]
						}]
					}
					this.optionTwo = {
						title: {
							text: 'ECharts 入门示例'
						},
						tooltip: {},
						legend: {
							data:['销量']
						},
						xAxis: {
							data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
						},
						yAxis: {},
						series: [{
							name: '销量',
							type: 'bar',
							data: [50, 40, 36, 20, 10, 0]
						}]
					}
				} else {	// 点击偶数次加载这里的option 数值从低到高
					this.flag = true
					this.optionOne = {
						title: {
							text: 'ECharts 入门示例'
						},
						tooltip: {},
						legend: {
							data:['销量']
						},
						xAxis: {
							data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
						},
						yAxis: {},
						series: [{
							name: '销量',
							type: 'line',
							data: [0, 10, 20, 30, 40, 50]
						}]
					}
					
					// 如果注释掉下面optionTwo的赋值，会出现optionOne（线图）显示在optionTwo（本应该是柱状图）的图表上
					// 如果不注释掉，那么只有图表二会更新，其实是图表二先显示了optionOne然后瞬间被optionTwo的数据覆盖掉
					// 也就是说optionOne和optionTwo的数据都显示在了图表二上 图表一没有收到后续更新的optionOne数值
					
					this.optionTwo = {
						title: {
							text: 'ECharts 入门示例'
						},
						tooltip: {},
						legend: {
							data:['销量']
						},
						xAxis: {
							data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
						},
						yAxis: {},
						series: [{
							name: '销量',
							type: 'bar',
							data: [0, 10, 20, 30, 40, 50]
						}]
					}
					
				}
			}
		}
	}
</script>

<style>
	.content {
		flex: 1;
		justify-content: center;
		align-items: center;
	}

	.title {
		font-size: 36px;
		color: #8f8f94;
	}
	
	.page-body {
		height: 100%;
		margin: 0 30px;
		flex-grow: 1;
		flex-direction: column;
		overflow-x: hidden;
	}

	.page-section {
		flex-direction: column;
		margin-bottom: 60px;
		background-color: rgba(255, 255, 255, 0.8);
	}
	
	.chart {
		width: 100%;
		height: 200px;
		border: 1px solid #000;
	}
</style>
