<template>
  <div ref="chartP" class="pie_chart">
    <div
      :id="wroldChartId"
      class="chart"
      ref="my_pie_chart"
      style="width: 100%; height: 100%"
    >
      图表
    </div>
  </div>
</template>

<script>
import continentObj from "../js/geoData";
export default {
  name: "World",
  components: {},
  props: {
    pieChartSimpleLegend: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      wroldChartId: "wroldChartId",
      myEchart: null,
    };
  },
  mounted() {
    this.getPieChatr();
  },
  methods: {
    getPieChatr() {
      let myEchart;
      let domEcharts = document.getElementById(this.wroldChartId);
      if (!domEcharts) return;
      this.$echarts.registerMap("continent", continentObj);
      myEchart = this.$echarts.init(domEcharts);
      let option = {
        tooltip: {
          trigger: "item",
          showDelay: 0,
          transitionDuration: 0.2,
          formatter: function (params) {
            var value = (params.value + "").split(".");
            value = value[0].replace(/(\d{1,3})(?=(?:\d{3})+(?!\d))/g, "$1,");
            return params.seriesName + "<br/>" + params.name + ": " + value;
          },
        },
        visualMap: {
          left: "right",
          min: 0,
          max: 500,
          inRange: {
            color: [
              "#eeeeee",
							// "#eafcfc",
              "#ccffff",
							// "#f4f4aa",
              "#ffff99",
							"#ff9966"
            ],
          },
          text: ["High", "Low"], // 文本，默认为数值文本
          calculable: true,
        },
        toolbox: {
          show: true,
          left: "left",
          top: "top",
          feature: {
            dataView: { readOnly: false },
            restore: {},
            saveAsImage: {},
          },
        },
        series: [
          {
            name: "2013年出境目的地（洲際統計）",
            type: "map",
            mapType: "continent", // 自定義擴展圖表類型
            itemStyle: {
              normal: { label: { show: true } },
              emphasis: { label: { show: true } },
            },
            data: [
							{ name: "欧洲", value: 183.62 },
              { name: "亚洲", value: 999.69 },
              { name: "非洲", value: 200.5837 },
              { name: "北美洲", value:87.63 },
              { name: "南美洲", value: 600.41 },
              { name: "大洋洲", value:0.09},
            ],
          },
        ],
      };
      myEchart.setOption(option);
    },
  },
};
</script>
<style  lang="scss" scoped>
.pie_chart {
  overflow: hidden;
  height: 100%;
  width: 100%;
  background: #fff;
  .chart {
    width: 100%;
    height: 100%;
  }
}
</style>
