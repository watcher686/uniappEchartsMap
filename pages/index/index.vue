<template>
	<view>
		<view class="wrap">
			<mpvue-echarts id="main" ref="mapChart" :echarts="echarts" @onInit="renderMap" />
		</view>
		<view>123</view>
	</view>
</template>

<script>
	import * as echarts from 'echarts/echarts.min.js'; /*echarts.min.js为在线定制*/
	import * as chinaJson from '../../echarts/map/json/china.json'; /*echart.min.js为在线定制*/
	import mpvueEcharts from 'mpvue-echarts';


	export default {
		data() {
			return {
				echarts,
				data: [{
						name: "南海诸岛",
						value: this.randomValue()
					},
					{
						name: '北京',
						value: this.randomValue()
					},
					{
						name: '天津',
						value: this.randomValue()
					},
					{
						name: '上海',
						value: this.randomValue()
					},
					{
						name: '重庆',
						value: this.randomValue()
					},
					{
						name: '河北',
						value: this.randomValue()
					},
					{
						name: '河南',
						value: this.randomValue()
					},
					{
						name: '云南',
						value: this.randomValue()
					},
					{
						name: '辽宁',
						value: this.randomValue()
					},
					{
						name: '黑龙江',
						value: this.randomValue()
					},
					{
						name: '湖南',
						value: this.randomValue()
					},
					{
						name: '安徽',
						value: this.randomValue()
					},
					{
						name: '山东',
						value: this.randomValue()
					},
					{
						name: '新疆',
						value: this.randomValue()
					},
					{
						name: '江苏',
						value: this.randomValue()
					},
					{
						name: '浙江',
						value: this.randomValue()
					},
					{
						name: '江西',
						value: this.randomValue()
					},
					{
						name: '湖北',
						value: this.randomValue()
					},
					{
						name: '广西',
						value: this.randomValue()
					},
					{
						name: '甘肃',
						value: this.randomValue()
					},
					{
						name: '山西',
						value: this.randomValue()
					},
					{
						name: '内蒙古',
						value: this.randomValue()
					},
					{
						name: '陕西',
						value: this.randomValue()
					},
					{
						name: '吉林',
						value: this.randomValue()
					},
					{
						name: '福建',
						value: this.randomValue()
					},
					{
						name: '贵州',
						value: this.randomValue()
					},
					{
						name: '广东',
						value: 20
					},
					{
						name: '青海',
						value: this.randomValue()
					},
					{
						name: '西藏',
						value: 0
					},
					{
						name: '四川',
						value: this.randomValue()
					},
					{
						name: '宁夏',
						value: this.randomValue()
					},
					{
						name: '海南',
						value: this.randomValue()
					},
					{
						name: '台湾',
						value: this.randomValue()
					},
					{
						name: '香港',
						value: this.randomValue()
					},
					{
						name: '澳门',
						value: this.randomValue()
					}
				]
			};
		},
		components: {
			mpvueEcharts
		},
		onLoad() {

		},
		methods: {
			randomValue() {
				return Math.round(Math.random() * 25);
			},
			renderMap(e) {
				const that = this;
				var mydata = that.data;
				let {
					canvas,
					width,
					height
				} = e;
				width = width - 20;
				echarts.setCanvasCreator(() => canvas);
				const chart = echarts.init(canvas, null, {
					width: width,
					height: height
				})
				echarts.registerMap('china', chinaJson);
				canvas.setChart(chart)
				var optionMap = {
					title: {
						text: '门店分布图',
						x: 'center'
					},
					tooltip: {
						trigger: 'item',
						formatter: '{b}:{c}家店'
					},
					//左侧小导航图标
					visualMap: {
						min: 0,
						max: 25,
						left: 'left',
						top: 'bottom',
						// orient:'horizontal',
						// text: ['高', '低'], //取值范围的文字
						inRange: {
							color: ['#fff8ed','#f2b95b'] //取值范围的颜色
						},
						show: true, //图注
						pieces: [ //自定义『分段式视觉映射组件（visualMapPiecewise）』的每一段的范围，以及每一段的文字，以及每一段的特别的样式
							{
								min: 0,
								max: 5,
								label: '0~5家'
							},
							{
								min: 5,
								max: 10,
								label: '5~10家'
							},
							{
								min: 10,
								max: 15,
								label: '10~15家'
							},
							{
								min: 15,
								max: 20,
								label: '15~20家'
							},
							{
								min: 20,
								max: 25,
								label: '20~25家'
							},
						],
						hoverLink: true,
						textStyle: {
							fontSize: 8
						},
					},
					geo: {
						map: 'china',
						roam: false, //不开启缩放和平移
						zoom: 1.2,//视角缩放比例
						label: {
							normal: {
								show: false,
								fontSize: 8,
								color: 'rgba(0, 0, 0, 0.5)' //文字颜色
							}
						},
						itemStyle: {
							normal: {
								borderColor: 'rgba(0, 0, 0, 0.2)' //省份边框颜色
							},
							emphasis: {
								areaColor: '#F3B329', //鼠标选择区域颜色
								shadowOffsetX: 0,
								shadowOffsetY: 0,
								shadowBlur: 20,
								borderWidth: 0,
								shadowColor: 'rgba(0, 0, 0, 0.2)' //选择后的边框阴影颜色
							}
						}
					},
					//配置属性
					series: [
						{
							type: 'map',
							geoIndex: 0,
							animation: false,
							data: mydata,
						}
					]
				};
				//初始化echarts实例
				chart.setOption(optionMap);
				this.$refs.mapChart.setChart(chart);
			}
		}
	};
</script>

<style scoped lang="scss">
	.wrap {
		width: 100%;
		height: 600rpx;
		border: 1rpx solid #ddd;
	}
</style>
