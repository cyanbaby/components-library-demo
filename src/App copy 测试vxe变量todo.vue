<template>

  <div id="app">
    <div>
      <vxe-toolbar>
        <template #buttons>
          <vxe-button @click="allAlign = 'left'">居左</vxe-button>
          <vxe-button @click="allAlign = 'center'">居中</vxe-button>
          <vxe-button @click="allAlign = 'right'">居右</vxe-button>
        </template>
      </vxe-toolbar>

      <vxe-table :align="allAlign" :data="tableData">
        <vxe-column type="seq" width="60"></vxe-column>
        <vxe-column field="name" title="Name"></vxe-column>
        <vxe-column field="sex" title="Sex"></vxe-column>
        <vxe-column field="age" title="Age"></vxe-column>
      </vxe-table>
    </div>

    <div>
      <vxe-form
        title-colon
        ref="formRef"
        title-align="right"
        title-width="100"
        :data="formData"
        :rules="formRules"
        :loading="loading"
        @submit="submitEvent"
        @reset="resetEvent"
      >
        <vxe-form-gather span="12">
          <vxe-form-item title="名称" field="name" span="24"></vxe-form-item>
          <vxe-form-item title="昵称" span="24">
            <template #title>
              <span style="color: red">自定义标题</span>
            </template>
            <template #default="{ data }">
              <span>自定义 {{ data.nickname }}</span>
            </template>
          </vxe-form-item>
          <vxe-form-item
            title="标题貌似有点长呢"
            field="sex"
            span="24"
            :item-render="{}"
            title-overflow
          >
            <template #default="params">
              <vxe-select
                v-model="params.data.sex"
                placeholder="请选择性别"
                clearable
                @change="changeEvent(params)"
              >
                <vxe-option value="1" label="女"></vxe-option>
                <vxe-option value="2" label="男"></vxe-option>
              </vxe-select>
            </template>
          </vxe-form-item>
          <vxe-form-item
            title="标题貌似有点长呢"
            field="age"
            span="24"
            :item-render="{}"
            title-overflow="title"
          >
            <template #default="params">
              <vxe-input
                v-model="params.data.age"
                type="integer"
                placeholder="请输入年龄"
                clearable
                @change="changeEvent(params)"
              ></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item
            title="标题貌似有点长呢"
            field="date"
            span="24"
            :item-render="{}"
            title-overflow="ellipsis"
          >
            <template #default="{ data }">
              <vxe-input
                v-model="data.date"
                type="date"
                placeholder="请选择日期"
                clearable
              ></vxe-input>
            </template>
          </vxe-form-item>
        </vxe-form-gather>
        <vxe-form-gather span="12">
          <vxe-form-item
            title="标题貌似有点长呢标题貌似有点长呢"
            field="address"
            span="24"
            :item-render="{}"
          >
            <template #default="{ data }">
              <vxe-textarea
                v-model="data.address"
                placeholder="请输入地址"
                size="medium"
                clearable
              ></vxe-textarea>
            </template>
          </vxe-form-item>
        </vxe-form-gather>
        <vxe-form-item align="center" span="24">
          <template #default>
            <vxe-button
              type="submit"
              status="primary"
              content="基本表单"
            ></vxe-button>
            <vxe-button type="reset" content="重置"></vxe-button>
          </template>
        </vxe-form-item>
      </vxe-form>
    </div>

    <div>
      <div style="background-color: var(--vxe-primary-color);">1111</div>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      // list: []
      list: ['a', 'b', 'c', 'd'],

      // vxe-table
      allAlign: null,
      tableData: [
        {
          id: 10001,
          name: 'Test1',
          role: 'Develop',
          sex: 'Man',
          age: 28,
          address: 'test abc'
        },
        {
          id: 10002,
          name: 'Test2',
          role: 'Test',
          sex: 'Women',
          age: 22,
          address: 'Guangzhou'
        },
        {
          id: 10003,
          name: 'Test3',
          role: 'PM',
          sex: 'Man',
          age: 32,
          address: 'Shanghai'
        },
        {
          id: 10004,
          name: 'Test4',
          role: 'Designer',
          sex: 'Women',
          age: 24,
          address: 'Shanghai'
        }
      ],

      // vxe-form start
      loading: false,
      formData: {
        name: 'test1',
        nickname: 'Testing',
        sex: '',
        age: 26,
        date: '',
        address: '左右布局'
      },
      formRules: {
        name: [
          { required: true, message: '请输入名称' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符' }
        ],
        sex: [{ required: true, message: '请选择性别' }],
        age: [
          { required: true, message: '请输入年龄' },
          {
            validator({ itemValue }) {
              // 自定义校验
              if (Number(itemValue) > 35 || Number(itemValue) < 18) {
                return new Error('年龄在 18 ~ 35 之间')
              }
            }
          }
        ],
        date: [{ required: true, message: '必填校验' }]
      },
      // ve-form end
    }
  },
}
</script>

<style>
@import url(./app.css);
</style>