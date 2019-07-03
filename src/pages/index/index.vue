<template>
  <div>
    <div class="userinfo">
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <view class="section tc">
      <video id="myVideo" :src="curSrc" controls></video>
      <view class="btn-area">
        <input bindblur="bindInputBlur"/>
        <button @click="bindSendDanmu">获取视频地址</button>
      </view>
    </view>
  </div>
</template>

<script>
import card from '@/components/card'
import serviceTest from 'xgplayer-service-miniprogram'

export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      token: ' ',
      curSrc: ' ',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      }
    }
  },

  components: {
    card
  },

  methods: {
    bindSendDanmu () {
      let self = this
      serviceTest.url(this.token).then(res => {
        console.log(res)
        self.curSrc = res.Data.PlayInfoList[0].MainPlayUrl
      })
    }
  },
  onLoad () {
    let self = this
    wx.request({
      url: 'http://vod-sdk-playground.snssdk.com/api/v1/get_top_play_auth_token?ak=AKLTMGYwNjQ2M2I5YTRiNDUzNmJjMmFhOWNiNDcxNzYxZDY&sk=0gqzE0ULU1jhHwFlAJL9YsPYYBaAbRscDz4QBnboiBfjGVSdD%2bkXee4ksTfuYA2z&vid=v02805c50000bicullbrm1nec75pjdu0', // 示例
      header: {
        'content-type': 'application/json'
      },
      success (res) {
        self.token = res.data
      }
    })
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

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all{
  width:7.5rem;
  height:1rem;
  background-color:blue;
}
.all:after{
  display:block;
  content:'';
  clear:both;
}
.left{
  float:left;
  width:3rem;
  height:1rem;
  background-color:red;
}

.right{
  float:left;
  width:4.5rem;
  height:1rem;
  background-color:green;
}
</style>
