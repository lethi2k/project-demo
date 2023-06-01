<template>
  <div class="login-warp controller">
    <div class="logo-container">
      <img
        class="logo"
        src="https://hindubabynames.info/downloads/wp-content/themes/hbn_download/download/social-media/facebook-logo.png"
        alt="Logo"
      />
    </div>
    <a-form @submit="onSubmit" :form="form">
      <a-form-item
        v-if="state.notice"
        :validateStatus="'error'"
        :help="state.notice"
      >
        <a-alert :message="state.notice" type="error" showIcon closable />
      </a-form-item>
      <a-form-item
        name="username"
        :rules="[
          { required: true, message: 'Please enter your username' },
          { type: 'email', message: 'Please enter a valid email' },
        ]"
      >
      <a-input v-model:value="state.username" @input="handleUsernameInput" placeholder="Username" />
      </a-form-item>
      <a-form-item>
        <a-input-password
          :model="state.password"
          placeholder="Password"
        />
      </a-form-item>
      <a-form-item>
        <a-button class="login-button" type="primary" html-type="submit"
          >Login</a-button
        >
      </a-form-item>
    </a-form>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import { Form, Input, Alert, Checkbox, Button } from 'ant-design-vue'

// meta
definePageMeta({
  layout:<any> 'none',
})

const form = ref<Form | null>(null)
const state = reactive({
  notice: '',
  username: '',
  password: '',
  autoLogin: true,
})

const handleUsernameInput = (e: any) => {
  state.username = e.target.value
}

const onSubmit = async () => {
  try {
    await form.value.validateFields()
    console.log('value collected ->', {
      username: state.username,
      password: state.password,
      autoLogin: state.autoLogin,
    })
    // Do something with the login credentials
  } catch (error) {
    console.log('Validation error', error)
  }
}
</script>

<style>
.controller {
  margin: 100px auto;
  max-width: 350px;
}

.logo-container {
  margin: 10px auto;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.logo {
  max-width: 100px;
}

.login-button {
  width: 100%;
}
</style>
