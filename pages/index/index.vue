<template>
  <view class="container">
    <view class="top">
      <view class="to">
        <text>{{temperature}}</text>
        <text>{{weather}}</text>
      </view>
      <view class="bo">
        <text>{{province}}·</text>
        <text>{{city}}·</text>
        <text>{{district}}</text>
      </view>
    </view>
    <view class="content">
      <view class="c1" @click="clickC1">
        <image :src="content[0].url" mode=""></image>
        <text>{{content[0].name}}</text>
      </view>
      <view class="c2" @click="clickC2">
        <image :src="content[1].url" mode=""></image>
        <text>{{content[1].name}}</text>
      </view>
      <view class="c3"  @click="clickC3">
        <image :src="content[2].url" mode=""></image>
        <text>{{content[2].name}}</text>
      </view>
      <view class="c4"  @click="clickC4">
        <image :src="content[3].url" mode=""></image>
        <text>{{content[3].name}}</text>
      </view>
      <view class="c5"  @click="clickC5">
        <image :src="content[4].url" mode=""></image>
        <text>{{content[4].name}}</text>
      </view>
      <view class="c6"  @click="clickC6">
        <image :src="content[5].url" mode=""></image>
        <text>{{content[5].name}}</text>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        province: '',
        city: '',
        district: '',
        temperature: '',
        weather: '',
        content: [{
            id: 1,
            name: '精神保健',
            url: '/static/index/know.png'
          },
          {
            id: 2,
            name: '健康保健',
            url: '/static/index/hos.png'
          },
          {
            id: 3,
            name: '活动出行',
            url: '/static/index/activ.png'
          },
          {
            id: 4,
            name: '日常饮食',
            url: '/static/index/vega.png'
          },
          {
            id: 5,
            name: '家政护理',
            url: '/static/index/mus.png'
          },
          {
            id: 6,
            name: '定制服务',
            url: '/static/index/my.png'
          }
        ]
      }
    },
    mounted() {
    },
    computed: {
        city1: function() {
        return this.city.substring(0, 2)
      }
    },
    onLoad() {
      this.getMap();
      this.getWeather();
    },
    methods: {
      async getMap() {
        const {
          data: res
        } = await uni.$http.get('https://apis.map.qq.com/ws/location/v1/ip?key=L7HBZ-XAIWJ-ZOKFV-K4AM5-GTDB7-LRFIC')
        this.province = res.result.ad_info.province
        this.city = res.result.ad_info.city
        this.district = res.result.ad_info.district
      },
      async getWeather() {
        const {
          data: res
        } = await uni.$http.get(`http://apis.juhe.cn/simpleWeather/query?city=上海&key=e127980c1196f1edae18609fc024fd51`)
        this.temperature = res.result.future[0].temperature
        this.weather = res.result.future[0].weather
      },
      clickC1() {
        uni.navigateTo({
          url:'/pages/know/know'
        })
      },
      clickC2() {
        uni.navigateTo({
          url:'/pages/hos/hos'
        })
      },
      clickC3() {
        uni.navigateTo({
          url:'/pages/activ/activ'
        })
      },
      clickC4() {
        uni.navigateTo({
          url:'/pages/vega/vega'
        })
      },
      clickC5() {
        uni.navigateTo({
          url:'/pages/mus/mus'
        })
      },
      clickC6() {
        uni.navigateTo({
          url:'/pages/my/my'
        })
      },
    }
  }
</script>

<style>
  body {
    background-color: #F8F8FF;
  }

  .container {
    padding: 20px;
    font-size: 14px;
    line-height: 24px;
  }

  .container .top {
    background-color: #78c1fe;
    width: 680rpx;
    height: 270rpx;
    display: flex;
    justify-content: space-between;
    border-radius: 15px;
    flex-direction: column;
  }
  
  .container .top .to {
    display: flex;
    justify-content: center;
    font-size: 50rpx;
    color: #FFFFFF;
    font-weight: bold;
    margin-top: 30px;
  }
  
  .container .top .to text {
    margin-left: 20px;
  }

  .container .top .bo {
    display: flex;
    justify-content: center;
    font-size: 50rpx;
    font-weight: bold;
    color: #FFFFFF;
    margin-bottom: 20px;
  }

  .content {
    width: 680rpx;
    height: 1050rpx;
    margin-top: 25px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  .content view {
    width: 330rpx;
    height: 330rpx;
    border-radius: 15px;
    font-size: 40rpx;
    text-align: center;
    font-weight: bold;
    color: #FFFFFF;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .content view image {
    display: block;
    width: 70px;
    height: 70px;
  }


  .content .c1 {
    background-color: #ff7f38;
  }

  .content .c2 {
    background-color: #00a8f3;
  }

  .content .c3 {
    background-color: #edc15a;
  }

  .content .c4 {
    background-color: #5dbe8a;
  }

  .content .c5 {
    background-color: #f1939c;
  }

  .content .c6 {
    background-color: #9768af;
  }
</style>
