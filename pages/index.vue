<template>
  <div>
    <h1 :style="{ fontSize: '30px' }">Dashboard</h1>
    <h4 :style="{ margin: '14px 0' }">Date 18/05/2023, Time: 10:30 AM VNT</h4>
    <hr />

    <div class="box-select d-flex">
      <div class="buy">
        <label for="">Currency Buy &nbsp;</label>
        <a-select
          v-model:value="currency"
          label-in-value
          style="width: 120px"
          :options="currencyData"
        ></a-select>
      </div>

      <div class="sell">
        <label for="">Currency Sell &nbsp;</label>
        <a-select
          v-model:value="currency"
          label-in-value
          style="width: 120px"
          :options="currencyData"
        ></a-select>
      </div>
    </div>

    <div class="box-button">
      <a-button type="primary" v-for="(button, key) in buttons" :key="key"
        >{{ button.title }}: {{ button.number }}</a-button
      >
    </div>

    <div class="public-sport-rate">
      <h1 :style="{ margin: '18px 0', fontSize: '24px' }">
        Top 3 Best Rate Route
      </h1>
      <Line
        id="my-chart-id"
        :options="options"
        :data="chartData"
        style="height: 200px"
      />

      <a-row :gutter="16" class="mt-5">
        <a-col :span="8">
          <a-card title="Rate Route 1" :bordered="true">
            <p>VND - USDT - Agent A</p>
            <p>USDT - SGD - Agent B</p>
            <p>VND - SGD: 17000</p>
          </a-card>
        </a-col>
        <a-col :span="8">
          <a-card title="Rate Route 2" :bordered="true">
            <p>VND - USDT - Agent B</p>
            <p>USDT - SGD - Agent C</p>
            <p>VND - SGD: 17500</p>
          </a-card>
        </a-col>
        <a-col :span="8">
          <a-card title="Rate Route 3" :bordered="true">
            <p>VND - USDT - Agent D</p>
            <p>USDT - SGD - Agent E</p>
            <p>VND - SGD: 18000</p>
          </a-card>
        </a-col>
      </a-row>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend,
} from 'chart.js'
import { Line } from 'vue-chartjs'
import ChartJSPluginDatalabels from 'chartjs-plugin-datalabels'

import { ref } from 'vue'

// composable
const { t } = useLang()

// meta
definePageMeta({
  layout: 'default',
})

const currency = ref({ value: 'vnd' })
ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend,
  ChartJSPluginDatalabels
)

// const datasets = [
//     {
//       label: 'Agent A',
//       backgroundColor: '#C1C1C1',
//       data: [3000,17000,4000]
//     },
//     {
//       label: 'Agent B',
//       backgroundColor: '#848383',
//       data: [4000, 3000, 5000],
//     },
//   ];

const datasets = [
  {
    label: 'Rate Route 1',
    data: [17000, 17100, 17300, 17400, 17500, 17600],
    fill: true,
    backgroundColor: 'green',
    borderColor: 'green',
    tension: 0.1
  },
  {
    label: 'Rate Route 2',
    data: [17600, 17700, 17600, 17300, 17200, 17100],
    fill: false,
    backgroundColor: 'yellow',
    borderColor: 'yellow',
    tension: 0.1
  },
  {
    label: 'Rate Route 3',
    data: [18000, 17900, 17800, 17700, 17600, 17400],
    fill: false,
    backgroundColor: 'orange',
    borderColor: 'orange',
    tension: 0.1
  },
]

const chartData = {
  labels: ['May 15', 'May 16', 'May 17', 'May 18', 'May 19', 'May 20'],

  datasets: datasets,
}

const options = {
  responsive: true,
  plugins: {
    legend: {
      display: true,
    },
    datalabels: {
      // formatter: function (value, context) {
      //   // console.log(context.chart.data.datasets[context.dataIndex]);
      //   // console.log(context.dataIndex);
      //   console.log(context.chart.data.datasets)

      //   return context.chart.data.datasets[0]?.label + ': ' + value
      //   // return context.chart.data.labels[context.dataIndex];
      // },
      align: 'top',
      // color: 'white',
      font: {
        size: 16,
      },
    },
  },
  scales: {
    y: {
      border: {
        color: '#8d8d8d',
      },
      ticks: {
        display: true, //this will remove only the label
      },
      grid: {
        display: false, // Loại bỏ đường viền lưới dọc trục x
      },
      title: {
        display: true,
        text: 'VND - SGD',
        color: 'black',
      },
      // display: false, // Hide Y axis labels
    },
    x: {
      border: {
        color: '#8d8d8d',
      },
      ticks: {
        display: true, //this will remove only the label
      },
      grid: {
        display: false, // Loại bỏ đường viền lưới dọc trục x
      },
      // title: {
      //   display: true,
      //   color: 'black',
      //   text: 'Agent',
      // },
      // display: false, // Hide X axis labels
    },
  },
}

const currencyData = ref([
  {
    value: 'vnd',
    label: 'VND',
  },
  {
    value: 'usd',
    label: 'USD',
  },
])

const buttons = [
  {
    title: 'Number of Banks',
    number: 2,
  },
  {
    title: 'Number of Public Sports',
    number: 3,
  },
  {
    title: 'Number of Crypto Exchanges',
    number: 2,
  },

  {
    title: 'Number of Private data',
    number: 2,
  },
]
</script>

<style>
.ant-checkbox-group {
  margin-top: 5px;
  margin-left: 15px;
}
#components-layout-demo-custom-trigger .trigger {
  font-size: 18px;
  line-height: 64px;
  padding: 0 24px;
  cursor: pointer;
  transition: color 0.3s;
}

#components-layout-demo-custom-trigger .trigger:hover {
  color: #1890ff;
}

#components-layout-demo-custom-trigger .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.3);
  margin: 16px;
}

.site-layout .site-layout-background {
  background: #fff;
}

.d-flex {
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
  flex-direction: row;
}

.profile {
  display: flex;
  align-items: center;
  margin-right: 20px;
}

.ant-layout-sider-children {
  min-height: 1000px;
}

.ml-auto {
  margin-left: auto;
}

.infor-topbar {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  align-content: center;
  align-items: center;
  margin-right: 20px;
}

.transition-language {
  margin-top: 4px;
}

.ant-layout-header {
  margin-left: 20px;
}

.box-select .buy {
  margin-right: 20px;
}

.box-button button {
  margin-right: 20px;
  margin-top: 20px;
}

.mt-5 {
  margin-top: 20px;
}
</style>
