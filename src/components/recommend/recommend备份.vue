<template>
  <div class="recommend">
    <div class="recommend-content">
        <div class="slider-wrapper" v-if="recommends.length">
          <slider>
            <div v-for="item in recommends">
              <a :href="item.linkUrl">
                <img :src="item.picUrl" alt=""/>
              </a>
            </div>
          </slider>
        </div>
        <div class="recommend-list">
          <h1 class="list-title">热门歌单推荐</h1>
          <ul>
            <li v-for="item in discList" class="item">
              <div class="icon">
                <img width="60" height="60" :src="item.imgurl">
              </div>
              <div class="text">
                <h2 class="name" v-html="item.creator.name"></h2>

                <p class="desc" v-html="item.dissname"></p>
              </div>
            </li>
          </ul>
        </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Slider from 'base/slider/slider'
  import { getRecommend,getDiscList } from 'api/recommend'
  import {ERR_OK} from 'api/config'
  import Scroll from 'base/scroll/scroll'

  export default {
    data() {
    return {
      recommends: {},
      discList: {}
    }
  },
  created() {
    this._getRecommend()
    this._getDiscList()
  },
  methods:{
    _getRecommend()
    {
      getRecommend().then((res) => {
        if (res.code === ERR_OK) {
          this.recommends = res.data.slider
        }
      })
    }
  ,
    _getDiscList()
    {
      getDiscList().then((res) => {
        if (res.code === ERR_OK) {
          this.discList = res.data.list
        }
      })
    }
  },
  components:{
    Slider,
      Scroll
  }
  }


</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable"

  .recommend
  position: fixed
  width:

  100
  %
  top:

  88
  px
  bottom:

  0
  .recommend-content
  height:

  100
  %
  overflow: hidden
  .slider-wrapper
  position: relative
  width:

  100
  %
  overflow: hidden
  .recommend-list
  .list-title
  height:

  65
  px
  line-height:

  65
  px
  text-align: center
  font-size:

  $
  font-size-medium
  color:

  $
  color-theme
  .item
  display: flex
  box-sizing: border-box
  align-items: center
  padding:

  0
  20
  px

  20
  px

  20
  px
  .icon
  flex:

  0
  0
  60
  px
  width:

  60
  px
  padding-right:

  20
  px
  .text
  display: flex
  flex-direction: column
  justify-content: center
  flex:

  1
  line-height:

  20
  px
  overflow: hidden
  font-size:

  $
  font-size-medium
  .name
  margin-bottom:

  10
  px
  color:

  $
  color-text
  .desc
  color:

  $
  color-text-d
  .loading-container
  position: absolute
  width:

  100
  %
  top:

  50
  %
  transform:

  translateY
  (
  -
  50
  %
  )
</style>
