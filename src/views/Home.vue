<template>
  <div class="container mx-auto flex">
    <div class="flex flex-col items-center box-border p-2">
      <a-card 
        v-for="(config, i) in configes"
        :key="i"
        :title="config.name" 
        class="w-96"
        hoverable
        @click="onChangeActive(i)"
      >
        <p>请求URL：<a-tag color="green">{{ config.rurl }}</a-tag></p>
        <p v-if="config.rtype">请求类型：<a-tag color="blue">{{ config.rtype.toUpperCase() }}</a-tag></p>
      </a-card>
    </div>
    <div class="flex-1 flex box-border p-2 border-l border-gray-200">
      <div class="w-full box-border p-2 bg-white shadow-sm">
        <a-form
          :model="formState"
          :label-col="{ span: 2 }"
        >
          <a-form-item label="名称" required>
            <a-input v-model:value="formState.name"></a-input>
          </a-form-item>
          <a-form-item label="请求URL" required>
            <a-input v-model:value="formState.rurl"></a-input>
          </a-form-item>
        </a-form>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref } from 'vue'

export default {
  setup() {
    const configes = reactive([
      {
        name: 'TestDemo',
        rurl: "/v2/list",
        rtype: 'get',
      }
    ])
    const formState = reactive({
      name: "",
      rurl: "",
      rtype: null
    })
    const activeIndex = ref(-1)

    const onChangeActive = (index) => {
      Object.assign(formState, configes[index])
      activeIndex.value = index
    }

    return {
      configes,
      formState,
      activeIndex,
      onChangeActive,
    }
  }
}
</script>