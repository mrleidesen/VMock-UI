<template>
  <div class="container mx-auto flex">
    <div class="flex flex-col items-center box-border p-2 bg-white shadow-sm">
      <a-card 
        v-for="(config, i) in configes"
        :key="i"
        :title="config.name" 
        class="w-96"
        style="margin-bottom: 14px !important"
        hoverable
        @click="onChangeActive(i)"
      >
        <p>请求URL：<a-tag color="green">{{ config.rurl }}</a-tag></p>
        <p v-if="config.rtype">请求类型：<a-tag color="blue">{{ config.rtype.toUpperCase() }}</a-tag></p>
      </a-card>

      <a-button 
        class="mt-2"
        type="primary" 
        @click="onAddConfig"
      >新增</a-button>
    </div>

    <div class="flex-1 flex box-border p-2">
      <div class="w-full box-border p-2 bg-white shadow-sm">
        <a-form
          :model="formState"
          :label-col="{ span: 2 }"
        >
          <a-form-item label="名称" required>
            <a-input v-model:value="formState.name" placeholder="该接口名称"></a-input>
          </a-form-item>
          <a-form-item label="请求URL" required>
            <a-input v-model:value="formState.rurl" placeholder="请求的接口地址"></a-input>
          </a-form-item>
          <a-form-item label="请求类型">
            <a-select v-model:value="formState.rtype" placeholder="不填默认拦截全部">
              <a-select-option value="">全部</a-select-option>
              <a-select-option 
                v-for="option in selectOptions.rtype"
                :key="option"
                :value="option"
              >{{ option.toUpperCase() }}</a-select-option>
            </a-select>
          </a-form-item>
          <a-divider>模板数据</a-divider>

          <a-row
            v-for="(item, idx) in formState.template"
            :key="idx"
          >
            <a-col :span="8">
              <a-form-item label="属性名" :labelCol="{ span: 5 }">
                <a-input v-model:value="item.keyName" placeholder="属性名"></a-input>
              </a-form-item>
            </a-col>
            <a-col :span="8">
              <a-form-item label="规则" :labelCol="{ span: 5 }">
                <a-input v-model:value="item.rule" placeholder="生成规则"></a-input>
              </a-form-item>
            </a-col>
            <a-col :span="8">
              <a-form-item label="值" :labelCol="{ span: 5 }">
                <a-select v-model:value="item.value" placeholder="属性值">
                  <a-select-option 
                    v-for="option in selectOptions.value"
                    :key="option"
                    :value="option"
                  >{{ option }}</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
          </a-row>

          <a-button class="mr-2" @click="onAddTemplate">添加模板字段</a-button>
          <a-button type="primary" @click="onSaveConfig">保存</a-button>
        </a-form>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref } from 'vue'

export default {
  setup() {
    const selectOptions = {
      rtype: ['get', 'post', 'put', 'delete'],
      type: ['String', 'Number', 'Array', 'Object'],
      value: ['@boolean()', '@natural()', '@integer()', '@float()', '@character()', '@string()', '@image()', '@date()', '@color()', '@paragraph()', '@cparagraph()', '@name()', '@cname()', '@url()', '@email()', '@id()', '@guid()']
    }
    const defaultTemplate = { keyName: 'data', rule: '1-10', value: "@string()" }
    const defaultConfig = {
      name: 'TestDemo',
      rurl: "/v2/list",
      rtype: '',
      template: [{ keyName: 'data', rule: '1-10', value: "@string()" }],
    }

    const configes = reactive([
      {
        name: 'TestDemo',
        rurl: "/v2/list",
        rtype: '',
        template: [{ keyName: 'data', rule: '1-10', value: "@string()" }],
      }
    ])
    const formState = reactive({
      name: "",
      rurl: "",
      rtype: "",
      template: []
    })
    const activeIndex = ref(-1)

    // methods
    const onChangeActive = (index) => {
      Object.assign(formState, configes[index])
      activeIndex.value = index
    }
    const onAddTemplate = () => {
      formState.template.push({...defaultTemplate})
    }
    const onAddConfig = () => {
      configes.push({...defaultConfig})
    }
    const onSaveConfig = () => {
      configes[activeIndex.value] = {...formState}
    }

    return {
      configes,
      formState,
      activeIndex,
      selectOptions,
      onChangeActive,
      onAddTemplate,
      onAddConfig,
      onSaveConfig
    }
  }
}
</script>
