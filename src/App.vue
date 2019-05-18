<template>
  <div id="app">
    <div class="demo">
      <section>
        <span>simple diff with image</span>
        <br>
        <br>
        <QuickDiff :origin="origin"
                   :diff="diff"
                   style="width: 540px; height: 400px">
        </QuickDiff>
      </section>

      <section>
        <span>diff image with a cursor</span>
        <br>
        <br>
        <QuickDiff :origin="origin"
                   :diff="diff"
                   cursor="circle"
                   style="width: 540px; height: 400px">
        </QuickDiff>
      </section>

      <section>
        <span>diff video with a cursor</span>
        <br>
        <br>
        <QuickDiff :origin="origin_video"
                   :diff="diff_video"
                   style="width: 480px; height: 360px">
        </QuickDiff>
      </section>

      <section>
        <span>auto diff video</span>
        <br>
        <br>
        <QuickDiff :origin="origin_video"
                   :diff="diff_video"
                   cursor="circle"
                   style="width: 480px; height: 360px">
        </QuickDiff>
      </section>


    </div>
  </div>
</template>

<script>
import  QuickDiff from './components/Component.vue'
export default {
  name: 'app',
  data(){
    return{
      origin: require("./assets/origin.jpg"),
      diff: require("./assets/diff.jpg"),
      origin_video: require("./assets/diff.mp4"),
      diff_video: require("./assets/origin.mp4")
    }
  },
  components: {
    QuickDiff
  }
}
</script>

<style lang="stylus" scoped>
  *{
    margin: 0;
    padding: 0;
  }

  #app {
    width: 100%;
    background-color: #fff;
    font-family: Tahoma, Helvetica, Arial, "Microsoft Yahei","微软雅黑", STXihei, "华文细黑", sans-serif;
    a{
      color: #42b883;
    }
  }

  .intro{
    width: 100%;
    text-align: center;
    margin-top: 80px;
  }

  .demo{
    width: 100%;
    padding: 20px;
    margin: 20px auto;
    background-color: #f9f9f9;
    text-align: center;

    section{
      width: 100%;
      text-align: center;
      padding: 36px;
      box-sizing: border-box;
      span{
        font-size: 18px;
        color: #42b883;
      }
      figure{
        margin 0auto;
      }
    }
  }
</style>
