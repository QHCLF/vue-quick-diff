# demo

![](./docs/demo/1.jpg) 
A component that can quickly see the difference between two pictures

## Installation
```
npm install --save vue-quick-diff
```

## How to use
```
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
```


## Props

 Name | Type | Default | Description
 ---- | ----- | ------ | ------
 width | real | null | Allow users to define their own width
 height | real | null | Allow users to define their own height
 posX | real | 200 | Define the initial position of the sliding bar
 pageX | real | null |Relative to pages and considering scrollbars
 isDragging | boolean | false | Actions used to judge animation
 allowNextFrame | boolean | true | Used to judge whether the action is over or not
 image_map | array | ['png', 'jpg', 'jpeg', 'gif']|Judging Picture Category
 video_map | array | ['webm', 'mp4', 'ogg']|Judging Video Category

