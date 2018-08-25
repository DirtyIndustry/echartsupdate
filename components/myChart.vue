<template>
	<!-- <view class="chart"> -->
	<mpvue-echarts :echarts="echarts" :onInit="handleInit" :canvasId="canvasId" ref="echartsRef"></mpvue-echarts>
	<!-- </view> -->
</template>

<script>
	import * as echarts from 'echarts'
	import mpvueEcharts from 'mpvue-echarts'

	let chart

	export default {
		name: 'myChart',
		props: {
			// 画布id 在页面中必须唯一
            canvasId: {
				type: String,
				default: 'id',
				required: true
            },
            // 图表数据
            option: {
                type: Object,
				default() {
					return {}
				},
				required: true
            }
		},
		data() {
			return {
				echarts
			}
		},
		computed: {
			thischart: function () {
				return chart
			}
		},
		watch: {
			option: {
                handler(newVal, oldVal) {
                    if (chart !== undefined) {
                        if (newVal) {
							// 两种更新数据的方法：
							
							// 一 setOption（）的方法
							// 用这种方法更新option会产生bug
							chart.setOption(newVal, true)
							
							// 二 重新init（）的方法
							// 用这种方法更新option没有bug，但是没有数据变化的动画
							// this.$refs.echartsRef.init()
							
							// 另外不知这两种方法哪个对系统负担比较小？目前项目中一个页面可能会用到五个图表
                        }
                    }
                }
            }
		},
		components: {
			mpvueEcharts
		},
		methods: {
			// 初始化图表
            handleInit(canvas, width, height) {
                chart = echarts.init(canvas, null, {
                    width: width,
                    height: height
                })
                canvas.setChart(chart)
                chart.setOption(this.option, false)
                return chart
            }
		},
	}
</script>

<style scoped>
	/* 曲线图的容器必须设置宽度和高度 */
    .chart {
        width: 100%;
        height: 200px;
        border: 1px solid #000000;
    }
</style>
