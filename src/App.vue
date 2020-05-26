<template>
  <div id="app">
    <header class="header-wrapper">
      <h1 class="title">echarts-数据可视化</h1>
      <!-- <span class="time">{{new Date()}}</span> -->
    </header>
    <section class="section-wrapper">
      <div class="section-one">
        <div class="panel-warpper">
          <h2>柱状图-访问量</h2>
          <div class="chart"
               ref="bar"></div>
          <div class="panel-footer"></div>
        </div>
        <div class="panel-warpper">
          <h2>折线图-访问量</h2>
          <div class="chart"
               ref="line"></div>
          <div class="panel-footer"></div>
        </div>
        <div class="panel-warpper">
          <h2>饼图-访问量</h2>
          <div class="chart"
               ref="pie"></div>
          <div class="panel-footer"></div>
        </div>
      </div>
      <div class="section-two">
        <div class="section-two-head-wrapper">
          <div class="head-number">
            <countTo :startVal='TCPnumber / 2'
                     :endVal='TCPnumber'
                     :duration='5000'></countTo>
            <countTo :startVal='UDPnumber / 2'
                     :endVal='UDPnumber'
                     :duration='5000'></countTo>
          </div>
          <div class="head-title">
            <span>TCP</span>
            <span>UDP</span>
          </div>
        </div>
        <div class="map">
          <div class="bg1"></div>
          <div class="bg2"></div>
          <div class="bg3"></div>
          <div class="map-charts"
               ref="map"></div>
        </div>
      </div>
      <div class="section-three">
        <div class="panel-warpper">
          <h2>柱状图-访问量</h2>
          <div class="chart"
               ref="bar2"></div>
          <div class="panel-footer"></div>
          <div class="panel-footer"></div>
        </div>
        <div class="panel-warpper">
          <h2>折线图-访问量</h2>
          <div class="chart"
               ref="line2"></div>
          <div class="panel-footer"></div>
          <div class="panel-footer"></div>
        </div>
        <div class="panel-warpper">
          <h2>饼图-访问量</h2>
          <div class="chart"
               ref="pie2"></div>
          <div class="panel-footer"></div>
          <div class="panel-footer"></div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import echarts from 'echarts';
import countTo from 'vue-count-to';
import '../public/lib/china.js';

const myColor = ["#1089E7", "#F57474", "#56D0E3", "#F8B448", "#8B78F6"];

const barOption = {
  color: ['#3398DB'],
  tooltip: {
    trigger: 'axis',
    axisPointer: {            // 坐标轴指示器，坐标轴触发有效
      type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
    }
  },
  grid: {
    top: '10px',
    left: '0%',
    right: '0%',
    bottom: '4%',
    containLabel: true
  },
  xAxis: [
    {
      type: 'category',
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
      axisTick: {
        alignWithLabel: true
      },
      axisLine: {
        show: false
      },
      axisLabel: {
        textStyle: {
          color: "rgba(255,255,255,.6)",
          fontSize: "12"
        }
      },
    }
  ],
  yAxis: [
    {
      type: 'value',
      axisLabel: {
        textStyle: {
          color: "rgba(255,255,255,.6)",
          fontSize: "12"
        }
      },
      axisLine: {
        lineStyle: {
          color: "rgba(255,255,255,.1)"
        }
      },
      splitLine: {
        lineStyle: {
          color: "rgba(255,255,255,.1)"
        }
      }
    }
  ],
  series: [
    {
      name: '直接访问',
      type: 'bar',
      barWidth: '40%',
      data: [10, 52, 200, 334, 390, 330, 220]
    }
  ]
}

const bar2Option = {
  color: ['#3398DB'],
  tooltip: {
    trigger: 'axis',
    axisPointer: {            // 坐标轴指示器，坐标轴触发有效
      type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
    }
  },
  grid: {
    top: '10px',
    left: '22%',
    bottom: '0',
    containLabel: false
  },
  yAxis: [
    {
      type: 'category',
      data: ["POST", "GET", "HEADE", "PUT", "DELETE"],
      axisTick: {
        show: false
      },
      axisLine: {
        show: false
      },
      splitLine: {
        show: false
      },
      axisLabel: {
        textStyle: {
          fontSize: 12,
          color: "#fff"
        }
      }
    },
    {
      type: 'category',
      axisTick: {
        show: false
      },
      axisLine: {
        show: false
      },
      splitLine: {
        show: false
      },
      axisLabel: {
        textStyle: {
          color: "rgba(255,255,255,.6)",
          fontSize: "12"
        }
      },

    }
  ],
  xAxis: [
    {
      show: false
    }
  ],
  series: [
    {
      name: '外层',
      type: 'bar',
      barWidth: '40%',
      data: [100, 100, 100, 100, 100],
      itemStyle: {
        color: 'none',
        borderColor: '#00c1de',
        barBorderRadius: 15
      },
      barCategoryGap: 50
    },
    {
      name: '内层',
      type: 'bar',
      yAxisIndex: 1,
      barWidth: '40%',
      data: [10, 20, 40, 80, 90],
      itemStyle: {
        barBorderRadius: 15,
        color: function (params) {
          let num = myColor.length;
          return myColor[params.dataIndex % num];
        }
      },
      label: {
        normal: {
          show: true,
          position: "inside",
          formatter: "{c}%"
        }
      }
    }
  ]
}

const lineOption = {
  tooltip: {
    trigger: 'axis'
  },
  xAxis: {
    data: [0, 2, 4, 6, 8, 12, 14, 16, 18, 20, 22],
    axisTick: {
      alignWithLabel: true
    },
    axisLine: {
      show: true,
      lineStyle: {
        color: "rgba(255,255,255,.1)"
      }
    },
    axisLabel: {
      textStyle: {
        color: "rgba(255,255,255,.6)",
        fontSize: "12"
      }
    },
  },
  grid: {
    top: '10px',
    left: '8%',
    right: '35%',
    bottom: '10%'
  },
  yAxis: {
    splitLine: {
      show: false
    },
    axisLabel: {
      textStyle: {
        color: "rgba(255,255,255,.6)",
        fontSize: "12"
      }
    },
    axisLine: {
      lineStyle: {
        color: "rgba(255,255,255,.1)"
      }
    }
  },
  visualMap: {
    top: 8,
    right: 8,
    pieces: [{
      gt: 0,
      lte: 50,
      color: '#096'
    }, {
      gt: 50,
      lte: 100,
      color: '#ffde33'
    }, {
      gt: 100,
      lte: 150,
      color: '#ff9933'
    }, {
      gt: 150,
      lte: 200,
      color: '#cc0033'
    }, {
      gt: 200,
      lte: 300,
      color: '#660099'
    }, {
      gt: 300,
      color: '#7e0023'
    }],
    outOfRange: {
      color: '#999'
    }
  },
  series: {
    name: 'TCP',
    type: 'line',
    data: [40, 60, 20, 100, 150, 190, 200, 160, 140, 105, 189, 240],
    markLine: {
      silent: true,
      data: [{
        yAxis: 50
      }, {
        yAxis: 100
      }, {
        yAxis: 150
      }, {
        yAxis: 200
      }, {
        yAxis: 300
      }]
    }
  }
}

const line2Option = {
  color: ['#00f2f1', '#ed3f35'],
  tooltip: {
    trigger: 'axis'
  },
  legend: {
    data: ['TCP', 'UDP']
  },
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: {
    type: 'category',
    boundaryGap: false,
    data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],
    axisLine: {
      show: true,
      lineStyle: {
        color: "rgba(255,255,255,.1)"
      }
    },
    axisLabel: {
      textStyle: {
        color: "rgba(255,255,255,.6)",
        fontSize: "12"
      }
    }
  },
  yAxis: {
    type: 'value',
    axisLine: {
      show: true,
      lineStyle: {
        color: "rgba(255,255,255,.1)"
      }
    },
    axisLabel: {
      textStyle: {
        color: "rgba(255,255,255,.6)",
        fontSize: "12"
      }
    },
    splitLine: {
      show: false
    },

  },
  series: [
    {
      name: 'TCP',
      type: 'line',
      data: [120, 132, 101, 134, 90, 230, 210],
      smooth: true
    },
    {
      name: 'UDP',
      type: 'line',
      data: [220, 182, 191, 234, 290, 330, 310],
      smooth: true
    }
  ]
}

const pieOption = {
  color: myColor,
  tooltip: {
    trigger: 'item',
    formatter: '{a} <br/>{b}: {c} ({d}%)'
  },
  legend: {
    bottom: '1%',
    data: ['POST', 'GET', 'PUT', 'HEAD', 'DELETE'],
    itemWidth: 10,
    itemHeight: 10
  },
  grid: {
    top: '10px',
    left: '4%',
    right: '4%',
    bottom: '4%'
  },
  series: [
    {
      name: '访问次数',
      type: 'pie',
      radius: ['50%', '70%'],
      avoidLabelOverlap: false,
      label: {
        show: false,
        position: 'center'
      },
      emphasis: {
        label: {
          show: true,
          fontSize: '20',
          fontWeight: 'bold'
        }
      },
      labelLine: {
        show: false
      },
      data: [
        { value: 335, name: 'POST' },
        { value: 310, name: 'GET' },
        { value: 234, name: 'PUT' },
        { value: 135, name: 'HEAD' },
        { value: 158, name: 'DELETE' }
      ]
    }
  ]
}

const pie2Option = {
  color: myColor,
  tooltip: {
    trigger: 'item',
    formatter: '{a} <br/>{b} : {c} ({d}%)'
  },

  visualMap: {
    show: false,
    min: 80,
    max: 600,
    inRange: {
      colorLightness: [0, 1]
    }
  },
  series: [
    {
      name: '访问来源',
      type: 'pie',
      radius: ['10%', '75%'],
      center: ['50%', '50%'],
      data: [
        { value: 335, name: 'TCP' },
        { value: 310, name: 'UDP' },
        { value: 274, name: 'HEAD' },
        { value: 235, name: 'PUT' },
        { value: 400, name: 'DELETE' }
      ].sort(function (a, b) { return a.value - b.value; }),
      roseType: 'radius',
      label: {
        color: 'rgba(255, 255, 255, 0.3)'
      },
      labelLine: {
        lineStyle: {
          color: 'rgba(255, 255, 255, 0.3)'
        },
        smooth: 0.2,
        length: 10,
        length2: 20
      },
      itemStyle: {
        shadowBlur: 200,
        shadowColor: 'rgba(0, 0, 0, 0.5)'
      },

      animationType: 'scale',
      animationEasing: 'elasticOut',
      animationDelay: function () {
        return Math.random() * 200;
      }
    }
  ]
}

const mapOption = {
  tooltip: {
    trigger: 'item',
    position: function (pos, params, dom, rect, size) {
      let obj = { top: 60 };
      obj[['left', 'right'][+(pos[0] < size.viewSize[0] / 2)]] = 5;
      return obj;
    },
    formatter: (data) => {
      return `${data.name}: ${isNaN(data.value) ? 0 : data.value}`
    }
  },
  visualMap: {
    min: 0,
    max: 1500,
    left: 'left',
    top: 'bottom',
    text: ['High', 'Low'],
    seriesIndex: [1],
    inRange: {
      color: ['blue', 'skyblue', 'red', 'yellow', 'pink', 'green'],
    },
    calculable: true
  },
  geo: {
    map: 'china',
    roam: true,
    label: {
      normal: {
        show: true,
        textStyle: {
          color: 'rgba(255,255,255,.6)'
        }
      }
    },
    itemStyle: {
      normal: {
        borderColor: 'rgba(0,193,222,.8)',
        areaColor: 'rgba(20,41,87,.8)'
      },
      emphasis: {
        areaColor: true,
        shadowOffsetX: 0,
        shadowOffsetY: 0,
        shadowBlur: 20,
        borderWidth: 0,
        shadowColor: 'rgba(0, 0, 0, 0.5)'
      }
    }
  },
  series: [
    {
      type: 'scatter',
      coordinateSystem: 'geo',
      symbolSize: 20,
      symbol: 'none',
      symbolRotate: 35,
      label: {
        normal: {
          formatter: '{b}',
          position: 'right',
          show: false
        },
        emphasis: {
          show: true
        }
      },
      itemStyle: {
        normal: {
          color: '#F06C00'
        }
      }
    },
    {
      name: 'categoryA',
      type: 'map',
      geoIndex: 0,
      data: [
        { name: '北京', value: '0' },
        { name: '天津', value: '111' },
        { name: '上海', value: '222' },
        { name: '重庆', value: '333' },
        { name: '河北', value: '444' },
        { name: '河南', value: '555' },
        { name: '云南', value: '666' },
        { name: '辽宁', value: '777' },
        { name: '黑龙江', value: '888' },
        { name: '湖南', value: '999' },
        { name: '安徽', value: '1111' },
        { name: '山东', value: '1500' },
      ]
    }
  ]
}

export default {
  name: 'App',
  components: { countTo },
  data () {
    return {
      echartsList: [],
      TCPnumber: 29348,
      UDPnumber: 43543,
      windowSet: {
        windowHeight: document.body.clientHeight,
        devicePixelRatio: window.devicePixelRatio
      }
    }
  },
  mounted () {
    let that = this;
    this.$nextTick(() => {
      const barEcharts = echarts.init(this.$refs.bar);
      barEcharts.setOption(barOption);
      this.echartsList.push(barEcharts);

      const bar2Echarts = echarts.init(this.$refs.bar2);
      bar2Echarts.setOption(bar2Option);
      this.echartsList.push(bar2Echarts);

      const lineEcharts = echarts.init(this.$refs.line);
      lineEcharts.setOption(lineOption);
      this.echartsList.push(lineEcharts);

      const line2Echarts = echarts.init(this.$refs.line2);
      line2Echarts.setOption(line2Option);
      this.echartsList.push(line2Echarts);

      const pieEcharts = echarts.init(this.$refs.pie);
      pieEcharts.setOption(pieOption);
      this.echartsList.push(pieEcharts);

      const pie2Echarts = echarts.init(this.$refs.pie2);
      pie2Echarts.setOption(pie2Option);
      this.echartsList.push(pie2Echarts);

      const mapEcharts = echarts.init(this.$refs.map);
      mapEcharts.setOption(mapOption);
      this.echartsList.push(mapEcharts);
    })

    window.onresize = () => { // 监听窗口高度变化
      return (() => {
        that.windowSet.windowHeight = document.body.clientHeight;
        that.windowSet.devicePixelRatio = window.devicePixelRatio;
      })();
    }
  },
  watch: {
    windowSet: {
      handler () {
        if (!this.timer) { // 避免频繁改动页面大小，造成卡顿
          this.timer = true;
          let that = this;
          this.echartsList.forEach(item => {
            item.resize();
          })
          setTimeout(function () {
            that.timer = false;
            console.log(1);
          }, 200);
        }
      },
      deep: true
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  line-height: 1.15;
  box-sizing: border-box;
}

@font-face {
  font-family: electronicFont;
  src: url(/font/DS-DIGIT.TTF);
}

#app {
  height: 100%;
  background: url(/images/bg.jpg) no-repeat #000;
  background-size: cover;
  overflow: hidden;
  .header-wrapper {
    height: 1.25rem;
    width: 100%;
    position: relative;
    background: url(/images/head_bg.png) no-repeat top center;
    background-size: 100% 100%;
    .title {
      font-size: 0.475rem;
      color: #ffffff;
      text-align: center;
      line-height: 1rem;
    }
    .time {
      position: absolute;
      bottom: 0.2rem;
      right: 0;
      color: #fff;
    }
  }
  .section-wrapper {
    display: flex;
    min-width: 1024px;
    max-width: 1920px;
    padding: 0.125rem 0.125rem 0;
    .section-one {
      flex: 3;
    }
    .section-two {
      flex: 5;
      padding: 0 0.25rem;
      &-head-wrapper {
        background: rgba(101, 132, 226, 0.1);
        padding: 0.1875rem;
        .head-number {
          display: flex;
          position: relative;
          width: 100%;
          border: 1px solid rgba(25, 186, 139, 0.17);
          & > span {
            flex: 1;
            text-align: center;
            height: 1rem;
            line-height: 1rem;
            font-size: 0.875rem;
            color: #ffeb7b;
            padding: 0.05rem 0;
            font-family: electronicFont;
            font-weight: bold;
            &:first-child::after {
              content: "";
              position: absolute;
              height: 50%;
              width: 1px;
              background: rgba(255, 255, 255, 0.2);
              right: 50%;
              top: 25%;
            }
          }
          &::before {
            content: "";
            position: absolute;
            width: 30px;
            height: 10px;
            border-top: 2px solid #02a6b5;
            border-left: 2px solid #02a6b5;
            top: 0;
            left: 0;
          }
          &::after {
            content: "";
            position: absolute;
            width: 30px;
            height: 10px;
            border-bottom: 2px solid #02a6b5;
            border-right: 2px solid #02a6b5;
            right: 0;
            bottom: 0;
          }
        }
        .head-title {
          display: flex;
          & > span {
            flex: 1;
            height: 0.5rem;
            line-height: 0.5rem;
            text-align: center;
            font-size: 0.225rem;
            color: rgba(255, 255, 255, 0.7);
            padding-top: 0.125rem;
          }
        }
      }
      .map {
        position: relative;
        height: 10.125rem;
        .bg1,
        .bg2,
        .bg3 {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          width: 6.475rem;
          height: 6.475rem;
          background: url(/images/map.png) no-repeat;
          background-size: 100% 100%;
          opacity: 0.3;
        }
        .bg2 {
          width: 8.0375rem;
          height: 8.0375rem;
          background-image: url(/images/lbx.png);
          opacity: 0.6;
          animation: rotate 15s linear infinite;
          z-index: 2;
        }
        .bg3 {
          width: 7.075rem;
          height: 7.075rem;
          background-image: url(/images/jt.png);
          animation: rotate 10s linear infinite reverse;
        }
        .map-charts {
          height: 100%;
          z-index: 300;
        }
        @keyframes rotate {
          from {
            transform: translate(-50%, -50%) rotate(0deg);
          }
          to {
            transform: translate(-50%, -50%) rotate(360deg);
          }
        }
      }
    }
    .section-three {
      flex: 3;
    }
  }

  .panel-warpper {
    position: relative;
    height: 3.875rem;
    border: 1px solid rgba(25, 186, 139, 0.17);
    background: rgba(255, 255, 255, 0.04) url(/images/line.png);
    padding: 0 0.1875rem 0.5rem;
    margin-bottom: 0.1875rem;
    &::before {
      position: absolute;
      top: 0;
      left: 0;
      content: "";
      width: 10px;
      height: 10px;
      border-top: 2px solid #02a6b5;
      border-left: 2px solid #02a6b5;
    }
    &::after {
      position: absolute;
      top: 0;
      right: 0;
      content: "";
      width: 10px;
      height: 10px;
      border-top: 2px solid #02a6b5;
      border-right: 2px solid #02a6b5;
    }
    .panel-footer {
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;
      &::before {
        position: absolute;
        bottom: 0;
        left: 0;
        content: "";
        width: 10px;
        height: 10px;
        border-bottom: 2px solid #02a6b5;
        border-left: 2px solid #02a6b5;
      }
      &::after {
        position: absolute;
        bottom: 0;
        right: 0;
        content: "";
        width: 10px;
        height: 10px;
        border-bottom: 2px solid #02a6b5;
        border-right: 2px solid #02a6b5;
      }
    }
    h2 {
      height: 0.6rem;
      line-height: 0.6rem;
      text-align: center;
      color: #fff;
      font-size: 0.25rem;
      font-weight: 400;
    }
    .chart {
      height: 3rem;
    }
  }
}
</style>
