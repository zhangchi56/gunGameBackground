<template>
  <div>
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="用户管理" name="first">
        <section class="yesterdayOrder">
          <div class="title">
            <span></span>截至昨日24:00
          </div>
          <div class="dataContainer">
            <div class="item">
              <div>有效订单</div>
              <div>￥98076.79</div>
              <div>100%</div>
            </div>
            <div class="item">
              <div>退款订单</div>
              <div>￥98076.79</div>
              <div>100%</div>
            </div>
            <div class="item">
              <div>退货订单</div>
              <div>￥98076.79</div>
              <div>100%</div>
            </div>
          </div>
        </section>
      </el-tab-pane>
      <el-tab-pane label="配置管理" name="second">用户增长</el-tab-pane>
      <el-tab-pane label="角色管理" name="third">活跃用户分析</el-tab-pane>
    </el-tabs>

    <!-- 2.为Echarts准备一个Dom -->
    <el-row style="margin-top:80px">
      <el-col :span="16">
        <div id="main" style="width: 1000px;height:600px;"></div>
      </el-col>
      <el-col :span="6"></el-col>
    </el-row>
  </div>
</template>

<script>
/*eslint-disable*/
// 1.导入echarts
import echarts from "echarts";

export default {
  data() {
    return {
      activeName: "first"
    };
  },
  created() {
    this.getEchartsList()
  },

  // 此时,页面上的元素,已经被渲染完毕了
  async mounted() {
    // 3.基于准备好的dom，初始化echarts实例
    var myChart = echarts.init(document.getElementById("main"));

    // 4.准备数据项和配置项
    // 指定图表的配置项和数据
    var option = {
      title: {
        text: "数据"
      },
      tooltip: {
        trigger: "axis"
      },
      legend: {
        data: ["昨日", "今日"]
      },
      grid: {
        left: "3%",
        right: "4%",
        bottom: "3%",
        containLabel: true
      },
      toolbox: {
        feature: {
          saveAsImage: {}
        }
      },
      xAxis: {
        type: "category",
        boundaryGap: false,
        data: ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15", "16","17", "18", "19", "20", "21","22","23/点"]
      },
      yAxis: {
        type: "value"
      },
      series: [
        {
          name: "昨日",
          type: "line",
          stack: "总量",
          data: [120, 132, 101, 134, 90, 230, 210]
        },
        {
          name: "今日",
          type: "line",
          stack: "总量",
          data: [220, 182, 191, 234, 290, 330, 310]
        }
      ]
    };
    // console.log(option.series)

    // 数据合并
    //  const result = _.merge(res.data, this.options)
    // 5.展示数据
    myChart.setOption(option);
    
  },
  methods: {
    //获取echarts数据
    async getEchartsList(){
       let res = await this.$http.get('http://120.25.234.158:9001/MemberQueryController/homeMemberData')
       console.log(res)
       
      //  this.option.series = [res.data.todayMemberList,res.data.yesterdayMemberList]
    },
    //切换tab
    handleClick(tab, event) {
      console.log(tab, event);
    }
  }
};
</script>

<style scope>
div {
  margin: 0;
  padding: 0;
}
.yesterdayOrder {
  margin-top: 20px;
}
.yesterdayOrder .title {
  font-size: 14px;
  display: flex;
  align-items: center;
  color: rgba(0, 0, 0, 0.65);
}
.yesterdayOrder .title span {
  margin-right: 10px;
  width: 5px;
  height: 20px;
  background-color: #00a2ae;
}
.yesterdayOrder .dataContainer {
  display: flex;
  margin-top: 20px;
}
.yesterdayOrder .dataContainer .item {
  padding: 40px;
  width: 300px;
  height: 200px;
}
.yesterdayOrder .dataContainer .item {
  margin-right: 20px;
  color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}
.yesterdayOrder .dataContainer .item:nth-child(1) {
  background-color: rgb(92, 184, 92);
}
.yesterdayOrder .dataContainer .item:nth-child(2) {
  background-color: rgb(91, 192, 222);
}
.yesterdayOrder .dataContainer .item:nth-child(3) {
  background-color: rgb(240, 173, 78);
}
.yesterdayOrder .dataContainer .item > div:first {
  font-size: 18px;
}
.yesterdayOrder .dataContainer .item > div:nth-child(2) {
  font-size: 25px;
}
.yesterdayOrder .dataContainer .item > div:nth-child(3) {
  font-size: 20px;
}
</style>
