<template>
<div>
  <a-row>
    <a-col :span="12"
      ><h1 :style="{ fontSize: '30px' }">Rates reference</h1>
      <h4 :style="{ margin: '14px 0' }">
        Date 18/05/2023, Time: 10:30 AM VNT
      </h4></a-col
    >
    <a-col :span="12">
      <div style="float: right">
        <label for="">Currency &nbsp;</label>

        <a-select
          v-model:value="currency"
          label-in-value
          style="width: 120px"
          :options="currencyData"
        ></a-select>
      </div>
    </a-col>
  </a-row>
  <hr />

  <div class="box-bank-rate">
    <h3 :style="{ margin: '18px 0' }">Bank Rate</h3>
    <a-row :style="{ margin: '18px 0' }">
      <a-col :span="8">
        <a-input :model="userName" placeholder="Search">
          <template #prefix>
            <user-outlined type="search blank" />
          </template>
          <template #suffix>
            <a-tooltip title="Extra information">
              <info-circle-outlined style="color: rgba(0, 0, 0, 0.45)" />
            </a-tooltip>
          </template>
        </a-input>
      </a-col>
      <a-col :span="16">
        <a-space :size="size" style="float: right">
          <a-button type="primary" class="mx-3">Export excel</a-button>
          <a-button type="primary">Refesh</a-button>
        </a-space>
      </a-col>
    </a-row>
    <a-table :columns="columns" :data-source="data" bordered />
  </div>

  <div class="public-sport-rate">
    <h3 :style="{ margin: '18px 0' }">Public Sport Rate</h3>
    <a-row :style="{ margin: '18px 0' }">
      <a-col :span="8">
        <a-input :model="userName" placeholder="Search">
          <template #prefix>
            <user-outlined type="search blank" />
          </template>
          <template #suffix>
            <a-tooltip title="Extra information">
              <info-circle-outlined style="color: rgba(0, 0, 0, 0.45)" />
            </a-tooltip>
          </template>
        </a-input>
      </a-col>
      <a-col :span="16">
        <a-space :size="size" style="float: right">
          <a-button type="primary" class="mx-3">Export excel</a-button>
          <a-button type="primary">Refesh</a-button>
        </a-space>
      </a-col>
    </a-row>
    <a-table :columns="columns" :data-source="data" bordered />
  </div>

  <div class="ctypto-exchange-rate">
    <h3 :style="{ margin: '18px 0' }">Ctypto Rxchange Rate</h3>
    <a-row :style="{ margin: '18px 0' }">
      <a-col :span="8">
        <a-input :model="userName" placeholder="Search">
          <template #prefix>
            <user-outlined type="search blank" />
          </template>
          <template #suffix>
            <a-tooltip title="Extra information">
              <info-circle-outlined style="color: rgba(0, 0, 0, 0.45)" />
            </a-tooltip>
          </template>
        </a-input>
      </a-col>
      <a-col :span="16">
        <a-space :size="size" style="float: right">
          <a-button type="primary" class="mx-3">Export excel</a-button>
          <a-button type="primary">Refesh</a-button>
        </a-space>
      </a-col>
    </a-row>
    <a-table :columns="columns" :data-source="data" bordered />
  </div>

  <div class="private-data-rate">
    <h3 :style="{ margin: '18px 0' }">Private Data Rate</h3>
    <a-row :style="{ margin: '18px 0' }">
      <a-col :span="12">
        <a-row>
          <a-col :span="16">
            <a-input :model="userName" placeholder="Search">
              <template #prefix>
                <user-outlined type="search blank" />
              </template>
              <template #suffix>
                <a-tooltip title="Extra information">
                  <info-circle-outlined style="color: rgba(0, 0, 0, 0.45)" />
                </a-tooltip>
              </template>
            </a-input>
          </a-col>

          <a-col :span="7">
            <a-checkbox-group :options="plainOptions" />
          </a-col>
        </a-row>
      </a-col>
      <a-col :span="12">
        <a-space :size="size" style="float: right">
          <a-button type="primary" class="mx-3">Export excel</a-button>
          <a-button type="primary">Refesh</a-button>
        </a-space>
      </a-col>
    </a-row>

    <h3>Fiat</h3>
    <a-table :columns="columns" :data-source="data" bordered />

    <h3>Ctypto</h3>
    <a-table :columns="columns" :data-source="data" bordered />
  </div>
</div>
</template>
<script lang="ts" setup>
import { defineComponent, ref } from 'vue'

// composable
const { t } = useLang()

// meta
definePageMeta({
  layout: 'default',
})
const userName = ref('')

const size = ref(8)
const currency = ref({ value: 'vnd' })
const localeSetting = useState('locale.setting')

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

const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
  },
  {
    title: 'Chinese Score',
    dataIndex: 'chinese',
    sorter: {
      compare: (a, b) => a.chinese - b.chinese,
      multiple: 3,
    },
  },
  {
    title: 'Math Score',
    dataIndex: 'math',
    sorter: {
      compare: (a, b) => a.math - b.math,
      multiple: 2,
    },
  },
  {
    title: 'English Score',
    dataIndex: 'english',
    sorter: {
      compare: (a, b) => a.english - b.english,
      multiple: 1,
    },
  },
]

const data = [
  {
    key: '1',
    name: 'John Brown',
    chinese: 98,
    math: 60,
    english: 70,
  },
  {
    key: '2',
    name: 'Jim Green',
    chinese: 98,
    math: 66,
    english: 89,
  },
  {
    key: '3',
    name: 'Joe Black',
    chinese: 98,
    math: 90,
    english: 70,
  },
  {
    key: '4',
    name: 'Jim Red',
    chinese: 88,
    math: 99,
    english: 89,
  },
]

const plainOptions = ['Fiat', 'Ctypto']
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
</style>
