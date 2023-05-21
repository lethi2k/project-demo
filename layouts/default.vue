<template>
  <a-layout>
    <a-layout-sider :model="collapsed" :trigger="null" collapsible>
      <div class="logo" />
      <a-menu :model="selectedKeys" theme="dark" mode="inline">
        <a-menu-item key="dashboard" @click="calculateQueryParams('/')">
          <user-outlined />
          <span>Dashboard</span>
        </a-menu-item>
        <a-menu-item
          key="rate-reference"
          @click="calculateQueryParams('/rate-reference')"
        >
          <video-camera-outlined />
          <span>Rate reference</span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout>
      <a-layout-header style="background: #fff; padding: 0">
        <div class="d-flex">
          <div class="trigger-menu">
            <menu-unfold-outlined
              v-if="collapsed"
              class="trigger"
              @click="() => (collapsed = !collapsed)"
            />
            <menu-fold-outlined
              v-else
              class="trigger"
              @click="() => (collapsed = !collapsed)"
            />
          </div>

          <div class="ml-auto infor-topbar">
            <div class="profile">
              <a-avatar-group>
                <a-avatar style="background-color: #1890ff">
                  <template #icon><UserOutlined /></template>
                </a-avatar>
              </a-avatar-group>
              <label for="">Han ping</label>
            </div>

            <ListboxButton
              type="button"
              title="Change Language"
              class="transition-language duration-300"
            >
              <span class="justify-center items-center flex">
                <IconLa:language />
              </span>
            </ListboxButton>
          </div>
        </div>
      </a-layout-header>
      <a-layout-content
        :style="{
          margin: '24px 16px',
          padding: '24px',
          background: '#fff',
          minHeight: '280px',
        }"
      >
        <slot />
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>

<script lang="ts" setup>
import {
  UserOutlined,
  VideoCameraOutlined,
  UploadOutlined,
  MenuUnfoldOutlined,
  MenuFoldOutlined,
} from '@ant-design/icons-vue'

const selectedKeys = ref(['dashboard'])
const collapsed = ref(false)

function calculateQueryParams(path: any) {
  const router = useRouter()
  router.push(path)
}
</script>
