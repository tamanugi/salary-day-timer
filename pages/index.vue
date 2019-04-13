<template lang="pug">
.container-wrapper
  .container
    section.title-wrapper
      .title #給料日はよタイマー
    section.content
      .left
        .hoge
          | 給料日
          .input-wrapper
            input(v-model="salaryDate" type="text" value="10")
          | 日まであと・・・

        .timer
          span.count {{ rest.seconds }}
          span.unit 秒

      .right
        img.salary-bag(src="~assets/background.png")

</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class extends Vue {
  salaryDate: number = 10
  rest: any = {seconds: -1}

  private timer: any

  mounted() {
    setInterval(() => {
      const target = new Date(2019, 5, this.salaryDate, 0, 0, 0).getTime()
      const now = new Date().getTime()
      const r = target - now
      this.rest.seconds = (r / 1000).toFixed(1)
    }, 100)
  }
}
</script>

<style lang="stylus" scoped>

@font-face {
  font-family: kfhimaji;
  src: url("~assets/fonts/KFhimaji.otf");
}

.title-wrapper
  display flex
  flex-direction  row
  justify-content flex-end

  .title
    margin-top 8px
    margin-right 24px
    font-size 24px
    color #404040
    opacity .2

/* Special */
.content
  font-size: 30px;
  line-height: 23px;
  display flex
  flex-direction row
  justify-content space-around
  align-content center
  align-items center
  
  .salary-bag
    width 270px
    height 510px


.container-wrapper
  display flex
  align-items center
  align-content center
  justify-content center
  height 100vh

.container
  font-family kfhimaji
  color #404040

  section
    margin-left 24px

.left

  margin-right 80px

  .hoge
    margin-bottom  50px
  .timer
    // position absolute
    // top 50%

    font-size 90px

    .unit
      margin-left 8px
      margin-right 16px
      font-size 32px

.input-wrapper
  display inline
  border-bottom solid #404040

  input
    border none
    background-color rgba(0, 0, 0, 0)
    font-size 32px
    width 48px
    margin 0 4px
    font-family kfhimaji
    color #404040
</style>
