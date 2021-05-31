<template>
  <div class="container mx-auto flex">
    <div class="w-1/2 flex flex-col items-center box-border p-2">
      <div 
        v-for="(config, i) in configes"
        :key="i"
        class="w-1/2 bg-white rounded-md overflow-hidden shadow flex flex-col box-border p-3 select-none cursor-pointer"
      >
        <h3 class="font-semibold text-gray-700 text-lg mb-2">{{ config.name }}</h3>
        <div 
          v-if="config.rurl" 
          class="flex items-center text-xs mb-1"
        >
          <span>接口地址：</span>
          <span class="bg-green-500 text-white p-1 rounded">{{ config.rurl }}</span>
        </div>
        <div 
          v-if="config.rtype" 
          class="flex items-center text-xs mb-1"
        >
          <span>请求类型：</span>
          <span class="bg-blue-500 text-white p-1 rounded">{{ config.rtype.toUpperCase() }}</span>
        </div>
      </div>
    </div>
    <div class="flex-1 flex box-border p-2 border-l border-gray-200">

    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'

export default {
  setup() {
    const configes = reactive([
      {
        name: 'TestDemo',
        rurl: "/v2/list",
        rtype: 'get',
      }
    ])

    return {
      configes
    }
  }
}
</script>