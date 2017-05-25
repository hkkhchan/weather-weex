<template>
  <div class="wrapper" @click="update">
    <image :src="logoUrl" class="logo"></image>
    <text class="title">{{today}}的天氣報告</text>
    <text class="title">{{weather}}</text>
  </div>
</template>

<style>
  .wrapper { align-items: center; margin-top: 120px; }
  .title { font-size: 48px; }
  .logo { width: 360px; height: 82px; }
</style>

<script>
  export default {
    data: {
      logoUrl: 'https://alibaba.github.io/weex/img/weex_logo_blue@3x.png',
      today: new Date().getMonth() + '月' + new Date().getDate() + '日',
      weather: ''
    },
    methods: {
      update: function (e) {
        console.log('Starting update');
        this.today='weather update:';
        let stream_module = require('@weex-module/stream');
        stream_module.fetch({
            method: 'GET',
            url: "http://php-kkhchan.rhcloud.com/download/wea.json",
            type: 'json'
        },function(res){
            self.weather=res.data;
        });
      }
    }
  }
</script>
