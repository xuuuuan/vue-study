<!--生命周期-->
<!--详情查看https://cn.vuejs.org/guide/essentials/lifecycle.html-->
<script setup lang="ts">
import { onMounted, ref } from 'vue';
import axios from 'axios';

const data = ref();

// 这里只演示了onMounted生命周期
onMounted(() => {
  let config = {
    method: 'get',
    maxBodyLength: Infinity,
    url: 'http://localhost:8090/api/v1/day/get?date=',
    headers: {
      userKey: 'cli_a7b88600e2877bd3c0b81e5e760885da',
      timestamp: '1684592953982',
      sign: '52595fd9990e68dd2f908ea35cacef1d',
    },
  };

  axios(config)
    .then((response) => {
      data.value = JSON.stringify(response.data.data, null, 2);
      console.log(data.value);
    })
    .catch((error) => {
      console.log(error);
    });
});
</script>

<template>
  <el-input type="textarea" rows="10" v-model="data"></el-input>
</template>

<style scoped></style>
