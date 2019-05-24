<template>
  <div class="mrsong">
    <slot>
      <div class="mr-year" v-if="isYear">
        <h1>年份倒计时</h1>
        <h2>{{timeText}}</h2>
      </div>
      <div class="mr-active" v-if="isActivity">
        <h1>活动倒计时</h1>
        <h2>{{activeText}}</h2>
      </div>
      <div class="mr-list" v-if="isList">
        <h1>列表倒计时</h1>
        <h2 v-for="(item,index) in listText" :key="index">{{item}}</h2>
      </div>
    </slot>
  </div>
</template>
<script>
  export default ({
    name: 'mrsongCountdown',
    // props: ['option', 'data'],
    props: {
      data: {
        type: Array,
        default () {
          return ['2019/10/8 08:18:08', '2019/11/8 08:28:08', '2019/12/8 08:08:08']
        }
      },
      activeTime: {
        type: String,
        default: '2018/8/8 08:08:08'
      },
      isActivity: {
        type: Boolean,
        default: true,
      },
      isYear: {
        type: Boolean,
        default: true,
      },
      isList: {
        type: Boolean,
        default: true,
      }
    },
    data() {
      return {
        timeText: '正在加载...',
        activeText: '正在加载...',
        listText: []
      }
    },
    mounted() {
      this.init()
    },
    methods: {
      getItem(e) {
        console.log(e);
      },
      init() {
        let that = this;
        let oDateNow = new Date();
        let activeTime = new Date(that.activeTime);
        that.data.map((item, index) => {
          let itemTime = new Date(item);
          return itemTime;
        })
        let oYear = oDateNow.getFullYear();
        let oDateEnd = new Date();
        oDateEnd.setFullYear(oYear + 1);
        oDateEnd.setMonth(0);
        oDateEnd.setDate(0);
        oDateEnd.setHours(0);
        oDateEnd.setMinutes(0);
        oDateEnd.setSeconds(0);
        function upDate() {
          //全年倒计时
          let oDateNow = new Date();
          let iTime = oDateEnd.getTime() - oDateNow.getTime();
          let iRemain = iTime / 1000;
          let iDay = parseInt(iRemain / 86400);
          iRemain %= 86400;
          let iHour = parseInt(iRemain / 3600);
          iRemain %= 3600;
          let iMin = parseInt(iRemain / 60);
          iRemain %= 60;
          let iSec = parseInt(iRemain);
          let timeText = oYear + "年还剩" + iDay + "天" + iHour + "时" + iMin + "分" + iSec + "秒";
          that.timeText = timeText;
          // 活动倒计时
          let aTime = activeTime.getTime() - oDateNow.getTime();
          let activeText = null;
          if (aTime > 0) {
            let aRemain = aTime / 1000;
            let aDay = parseInt(aRemain / 86400);
            aRemain %= 86400;
            let aHour = parseInt(aRemain / 3600);
            aRemain %= 3600;
            let aMin = parseInt(aRemain / 60);
            aRemain %= 60;
            let aSec = parseInt(aRemain);
            activeText = '距离活动结束还有' + aDay + "天" + aHour + "时" + aMin + "分" + aSec + "秒";
          } else {
            activeText = '活动结束';
          }
          that.activeText = activeText;
          // 列表倒计时
          let listText = that.data.map((item, index) => {
            // let itemTime = new Date(item); 
            let liTime = (new Date(item)).getTime() - oDateNow.getTime();
            let listText = null;
            if (liTime > 0) {
              let liRemain = liTime / 1000;
              let liDay = parseInt(liRemain / 86400);
              liRemain %= 86400;
              let liHour = parseInt(liRemain / 3600);
              liRemain %= 3600;
              let liMin = parseInt(liRemain / 60);
              liRemain %= 60;
              let liSec = parseInt(liRemain);
              listText = '距离活动结束还有' + liDay + "天" + liHour + "时" + liMin + "分" + liSec + "秒";
            } else {
              listText = '活动结束';
            }
            return listText;
          })
          let allData = {
            'timeText': that.isYear?timeText:null,
            'activeText': that.isActivity?activeText:null,
            'listText': that.isList?listText:null
          }
          that.listText = listText;
          that.$emit('sendData', allData)
        }
        setInterval(function() {
          upDate()
        }, 1000);
      }
    }
  })
</script>
<style lang="scss" scoped>
  * {
    margin: 0;
    padding: 0;
  }
  .swiper-wrapper {
    transition-timing-function: linear !important;
  }
  .swiper-slide {
    border: 1px solid #8888;
    .slide-item {
      min-height: 40px;
      line-height: 40px;
    }
  }
  .mr-active,.mr-list,.mr-year{
    margin: 20px;
    padding: 20px;
    background: #8888
  }
  .mr-list{
    h2{
      height: 40px;
      line-height: 40px;
    }
  }
</style>