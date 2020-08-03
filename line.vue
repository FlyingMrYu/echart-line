<template>
  <div class="line-chart-content">
    <div :id="'chartLineBox'+id" :style="{width: '100%',height: height}"></div>
  </div>
</template>
<script>
import echarts from "echarts";
import { mapState } from "vuex";
import { techRealtime } from "@/api/api";
export default {
  name: "lineChart",
  data() {
    return {
      loading: true //加载
    };
  },
  watch: {
    options: {
      deep: true,
      handler() {
        let self = this;
        self.drawchart();
      }
    }
  },
  props: ["id", "height", "type", "name", "info", "current", "options","toolbarShow"],
  methods: {
    //工艺绘制
    drawchart() {
      let chartLine = echarts.init(
        document.getElementById(`chartLineBox${this.id}`)
      );
      // 使用刚指定的配置项和数据显示图表。
      if (this.options) {
        if (this.toolbarShow) {
          let toolbox = {
            top: 0,
            right: 20,
            feature: {
              saveAsImage: {}
            }
          };
          this.options.toolbox = toolbox;
        }
        chartLine.setOption(this.options);
        window.onresize = function() {
          chartLine.resize();
          //myChart1.resize();    //若有多个图表变动，可多写
        };
      }
    }
  }
};
</script>

<style scoped lang="scss">
.line-chart-content {
  width: 100%;
  height: 100%;
}
</style>
