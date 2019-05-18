<template>
  <figure class="media-diff"
          @mousemove.prevent = "onMouseMove"
          @touchstart = "onMouseMove($event, true)"
          @touchmove = "onMouseMove($event, true)"
          @click = "onMouseMove($event, true)">
    <div class="origin-wrapper" :style="{ width: posX + 'px' }" @mousedown.prevent="onMouseDown">
      <img :src="origin" v-if="dtype==1" :style="{ width: width + 'px' }"/>
      <video muted :src="origin" v-if="dtype==-1" :style="{ width: width + 'px' }" autoplay loop="loop"></video>
    </div>

    <img :src="diff" v-if="dtype==1"/>
    <video muted :src="diff" v-if="dtype==-1" autoplay loop="loop"></video>
    <div class="handle" @mousedown.prevent="onMouseDown" :style="{ left: posX + 'px' }">
      <div class="cursor" v-if="cursor">
        <div class="circle">
        </div>
      </div>
    </div>

  </figure>
</template>

<script>
  export default {
    props: {
      origin: String,
      diff: String,
      cursor: String,
    },
    data() {
      return {
        width: null,
        height: null,
        posX: 200,
        pageX: null,
        isDragging: false,
        allowNextFrame: true,
        image_map: ['png', 'jpg', 'jpeg', 'gif'],
        video_map: ['webm', 'mp4', 'ogg']
      }
    },
    computed: {
      dtype: function () {
        let origin_dtype = this.computerDtype(this.origin);
        let diff_dtype = this.computerDtype(this.diff);
        return origin_dtype === diff_dtype ? origin_dtype : 0;
      }
    },
    methods: {
      computerDtype(val) {//判断是图片还是视频
        let extension = val.split('.').pop();
        return (this.image_map.indexOf(extension) - this.video_map.indexOf(extension))/2;
      },

      onResize() {//自适应窗口大小
        this.width = this.$el.clientWidth;
        this.height = this.$el.clientHeight;
      },

      updatePos() {
        this.posX = this.pageX - this.$el.getBoundingClientRect().left;
        if (this.posX < 0) this.posX = 0;
        if (this.posX > this.width) this.posX = this.width;
        this.allowNextFrame = true;
      },
      onMouseDown() {
        this.isDragging = true;
      },

      onMouseUp(event) {
        event.preventDefault();
        this.isDragging = false;
      },
      onMouseMove(event, isDragging = this.isDragging) {
        if (isDragging && this.allowNextFrame) {
          this.allowNextFrame = false;
          this.pageX = event.pageX || event.targetTouches[0].pageX || event.originalEvent.targetTouches[0].pageX;
          window.requestAnimationFrame(this.updatePos);
        }
      }
    },
    created() {
      window.addEventListener('mouseup', this.onMouseUp);
    },
    mounted() {
      this.onResize();
    },
    beforeDestroy() {
      window.removeEventListener('mouseup', this.onMouseUp);
    }
  }
</script>

<style lang="stylus">
  .media-diff{
    position: relative;
    margin: 0 auto;

    video, img{
      display: block;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }
  }

  .origin-wrapper {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    z-index: 1;
    transform: translateZ(0);
    will-change: width;
  }

  .handle{
    position: absolute;
    top: 0;
    bottom: 0;
    color: rgba(255, 255, 255, 0.80);
    background-color: rgba(255, 255, 255, 0.80);;
    width: 2px;
    cursor: ew-resize;
    transform: translateX(-50%) translateZ(0);
    z-index: 2;
    will-change: left;
    left: 200px;
  }

  .cursor{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translateX(-50%) translateZ(0);
    .circle {
      background-color: rgba(255, 255, 255, 0.80);
      width: 24px;
      height: 24px;
      border-radius: 50%;
    }
  }
</style>
