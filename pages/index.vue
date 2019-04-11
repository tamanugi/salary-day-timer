<template lang="pug">
header.container
  section.content
    | 給料日
    input.input-element(v-model="salaryDate" type="text" value="10")
    | まであと・・・

  section.timer
    span.count {{ rest.minutes }}
    span.unit 分
    span.count {{ rest.seconds }}
    span.unit 秒
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class extends Vue {
  salaryDate: number = 10
  rest: any = {minutes: 99999, seconds: 99}

  private timer: any

  mounted() {
    setInterval(() => {
      const target = new Date(2019, 5, this.salaryDate, 0, 0, 0).getTime() / 1000
      const now = new Date().getTime() / 1000
      const r = target - now
      this.rest.minutes = Math.floor( r / 60 )
      this.rest.seconds = Math.floor( r % 60 )
    }, 1000)
  }
}
</script>

<style lang="stylus">

@font-face {
  font-family: kfhimaji;
  src: url("~assets/fonts/KFhimaji.otf");
}

html, body, .container {
  height: 100%;
}

/* Reset */
html, body, h1, p, a, div, section {
  margin: 0;
  padding: 0;
  font-size: 100%;
  font: inherit;
}

/* Special */
.content
  position absolute
  top 40%
  // margin-left 55px;
  font-size: 30px;
  line-height: 23px;

body
  background-image url("~assets/background.png") 
  background-position center center
  /* コンテンツの高さが画像の高さより大きい時、動かないように固定 */
  background-attachment fixed
  /* 画像を常に天地左右の中央に配置 */
  background-position center center
   
  /* 画像をタイル状に繰り返し表示しない */
  background-repeat no-repeat
   
  /* 表示するコンテナの大きさに基づいて、背景画像を調整 */
  background-size contain

  margin auto
  width 1280px

  font-family kfhimaji
  color #404040

// .container
//   margin 0 auto
//   width 1280px

.timer
  position absolute
  top 50%

  font-size 90px

  .unit
    margin-left 8px
    margin-right 16px
    font-size 32px

.input-element
  border none
  background-color rgba(0, 0, 0, 0)
  font-size 32px
  width 48px
  margin 0 8px
  font-family kfhimaji
</style>
