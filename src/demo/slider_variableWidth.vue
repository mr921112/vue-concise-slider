<style lang="sass">
@import "../utils/common.scss"
</style>
<template>
  <div>
    <div style="width:70%;margin:20px auto;height:400px">
      <slider :pages="someList" :sliderinit="sliderinit" @slide='slide' @tap='onTap' @init='onInit'>
        <div slot="loading">
          <div class="loadingDot">
            <i></i>
            <i></i>
            <i></i>
            <i></i>
          </div>
        </div>
      </slider>
    </div>
    <div class="sliderButton">
      <button @click="slidePre">上一页</button>
      <button @click="slideNext">下一页</button>
      <button @click="appendslider">添加一页</button>
      <button @click="turnTo(2)">跳转到第三页</button>
      <button @click="autoplayStart">启动自动滚动</button>
      <button @click="autoplayStop">停止自动滚动</button>
    </div>
  </div>
</template>
<script>
import slider from '../components/slider'
export default {
  el: '#slidervariableWidth',
  data () {
    return {
      someList: [],
      sliderinit: {
        currentPage: 1,
        tracking: false,
        thresholdDistance: 100, // 滑动距离阈值判定
        thresholdTime: 300 // 滑动时间阈值判定
        // 不定宽度的无限循环感觉很丑:(
        // loop:true, // 无限循环
        // autoplay:1000 // 自动播放:时间[ms]
      }
    }
  },
  mounted () {
    let that = this
    setTimeout(function () {
      that.someList = [
        {
          html: 'slide1',
          style: {
            'background': '#1bbc9b',
            'width': '80%',
            'margin-right': '20px'
          }
        },
        {
          html: 'slide2',
          style: {
            'background': '#4bbfc3',
            'width': '60%',
            'margin-right': '20px'
          }
        },
        {
          html: 'slide3',
          style: {
            'background': '#7baabe',
            'width': '40%',
            'margin-right': '20px'
          }
        }
      ]
    }, 2000)
  },
  components: {
    slider
  },
  methods: {
    turnTo (num) {
      // 传递事件 vue 2.0 传递事件修改了，好的写法应该直接写在空vue类中
      this.$children[0].$emit('slideTo', num)
    },
    slideNext () {
      this.$children[0].$emit('slideNext')
      // slider.$emit('slideNext')
    },
    slidePre () {
      this.$children[0].$emit('slidePre')
      // slider.$emit('slidePre')
    },
    autoplayStart () {
      this.$children[0].$emit('autoplayStart')
      // slider.$emit('slidePre')
    },
    autoplayStop () {
      this.$children[0].$emit('autoplayStop')
      // slider.$emit('slidePre')
    },
    appendslider () {
      this.someList.push({
        html: 'slidernew',
        style: {
          background: '#333',
          color: '#fff'
        }
      })
    },
    // 监听事件发生了变化,需要指向一个子组件实例
    slide (data) {
      console.log(data)
    },
    onTap (data) {
      console.log(data)
    },
    onInit (data) {
      console.log(data)
    }
  }
}
</script>
