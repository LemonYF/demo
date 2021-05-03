<template>
  <div @click="clickHandle">
    <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
      <block v-for="(item, index) in images" :key="index">
        <swiper-item>
          <image :src="item" class="slide-image" mode="aspectFill"/>
        </swiper-item>
      </block>
    </swiper>
    <div class="menu-title">
      <ul class="tips">
        <li><i class="iconfont icon-icon6"> 免费</i></li>
        <li><i class="iconfont icon-icon6"> 迅速</i></li>
        <li><i class="iconfont icon-icon6"> 多品类</i></li>
      </ul>
    </div>
    <div>
      <ul class="pro-list">
        <li class="pro-item" v-for="(item, key) in proList" :key="id">
          <img src="https://android-artworks.25pp.com/fs08/2019/07/16/5/110_481c439b99996f63a2f57287c136d107_con.png" alt="">
          <p>是否订阅</p>
        </li>
      </ul>
    </div>
    <button open-type="getUserInfo" @getuserinfo="bindgetuserinfo">用户授权</button>
    <div class="userinfo" @click="getUserOpenInfo">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <img class="userinfo-avatar" src="/static/images/1.png" background-size="cover" />

      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <!--<div class="usermotto">-->
      <!--<div class="user-motto">-->
        <!--<card :text="motto"></card>-->
      <!--</div>-->
    <!--</div>-->

    <!--<form class="form-container">-->
      <!--<input type="text" class="form-control" :value="motto" placeholder="v-model" />-->
      <!--<input type="text" class="form-control" v-model="motto" placeholder="v-model" />-->
      <!--<input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />-->
    <!--</form>-->

    <!--<a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>-->

    <!--<div class="all">-->
        <!--<div class="left">-->
        <!--</div>-->
        <!--<div class="right">-->
        <!--</div>-->
    <!--</div>-->
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/img/logo.0aaccdfd.png'
      },
      indicatorDots: true,
      autoplay: true,
      interval: 3000,
      duration: 500,
      images: ['/static/images/1.png', '/static/images/2.png', '/static/images/1.png'],
      proList: [{
        id: 1
      }, {
        id: 2
      }, {
        id: 3
      }, {
        id: 4
      }]
    }
  },

  components: {
    card
  },
  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    bindgetuserinfo (e) {
      console.log(e)
    },
    getUserOpenInfo (e) {
      console.log('get user info')
      let that = this
      // console.log(e)
      // 获取用户信息
      wx.getSetting({
        success (res) {
          // console.log("res", res)
          if (res.authSetting['scope.userInfo']) {
            console.log('已授权')
            // 已经授权，可以直接调用 getUserInfo 获取头像昵称
            wx.getUserInfo({
              success (res) {
                console.log('获取用户信息成功', res)
                // that.setData({
                //   name: res.userInfo.nickName
                // })
              },
              fail (res) {
                console.log('获取用户信息失败', res)
              }
            })
          } else {
            console.log('未授权')
            that.showSettingToast('请授权')
          }
        }
      })
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.swiper {
  height: 376rpx !important;
}
image {
  width: 100%;
}

.menu-title{
  height: 100rpx;
  width: 100%;
  background: #ecf0f1;
  display: flex;
  align-items: center;
}
.tips {
  width: 100%;
  display: flex;
  justify-content: center !important;
}
  li  {
    width: 300rpx;
    height: 50rpx;
    padding: 0 28rpx;
  }
  li .iconfont {
    font-size: 20px !important;
    width: 180rpx;
  }
  .pro-list {
    width: 88%;
    height: 54vh;
    background-color: #ecf0f1;
    margin: 20rpx auto;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  .pro-item {
    width: 230rpx;
    height: 230rpx;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .pro-item >img {
    height: 160rpx;
    width: 160rpx;
  }
</style>
