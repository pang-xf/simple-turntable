<route lang="json5">
{
  layout: 'demo',
  style: {
    navigationBarTitleText: '请求',
  },
}
</route>

<template>
  <view class="p-6 text-center">
    <view class="my-2">使用的是 laf 云后台</view>
    <view class="text-green-400">我的推荐码，可以获得佣金</view>

    <!-- #ifdef H5 -->
    <view class="my-2">
      <a class="my-2" :href="recommendUrl" target="_blank">{{ recommendUrl }}</a>
    </view>
    <!-- #endif -->

    <!-- #ifndef H5 -->
    <view class="my-2 text-left text-sm">{{ recommendUrl }}</view>
    <!-- #endif -->

    <!-- http://localhost:9000/#/pages/index/request -->
    <button @click="getFoo" class="my-6">1.测试 GET 请求</button>
    <view class="text-xl">请求数据如下</view>
    <view class="text-green h-10">{{ JSON.stringify(data) }}</view>
    <view class="text-xl">完整数据</view>
    <view class="text-green h-16">{{ JSON.stringify(originalData) }}</view>
    <button @click="postFoo" class="my-6">2.测试 POST 请求</button>
    <view class="text-xl">请求数据如下</view>
    <view class="text-green h-10">{{ JSON.stringify(data2) }}</view>
    <button class="my-6" type="warn" @click="reset">3.一键清空数据</button>
  </view>
</template>

<script lang="ts" setup>
import { getFooAPI, postFooAPI, IFooItem } from '@/service/index/foo'

const recommendUrl = ref('http://laf.run/signup?code=ohaOgIX')

onLoad(() => {
  getFoo()
  postFoo()
})

const originalData = ref<IResData<IFooItem>>()
const data = ref<IFooItem>()
const getFoo = async () => {
  const res = await getFooAPI('菲鸽')
  data.value = res.data
  originalData.value = res
}

const data2 = ref<IFooItem>()
const postFoo = async () => {
  const res = await postFooAPI('菲鸽2')
  data2.value = res.data
}

const reset = () => {
  data.value = undefined
  data2.value = undefined
  originalData.value = undefined
}
</script>
