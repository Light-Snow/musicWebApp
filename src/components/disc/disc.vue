<template>
  <transition name="slide">
    <music-list :songs="songs" :title="title" :bg-image="bgImage"></music-list>
  </transition>


</template>

<script type="text/ecmascript-6">
  import musicList from 'components/music-list/music-list'
  import {mapGetters} from 'vuex'
  import {getSongList} from 'api/recommend'
  import {ERR_OK} from 'api/config'
  export default {
    data() {
      return {
        songs: []
      }
    },
    computed: {
      title() {
        return this.disc.dissname
      },
      bgImage() {
        return this.disc.imgurl
      },
      ...mapGetters([
        'disc'
      ])
    },
    created() {
      this._getSongList()
    },
    methods: {
      _getSongList() {
        console.log(this.disc.dissid)
        getSongList(this.disc.dissid).then((res) => {
          if (res.code === ERR_OK) {
            console.log(res.code)
            console.log(res.cdlist[0])
          }
        })
      }
    },
    components: {
      musicList
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable"
  .singer-detail
      position :fixed
      top: 0
      bottom 0
      right 0
      left 0
      z-index 100
      background $color-background
  .slide-enter-active,.slide-leave-active
      transition all 0.3s
  .slide-enter,.slide-leave-to
      transform translate3d(100%,0,0)
</style>
