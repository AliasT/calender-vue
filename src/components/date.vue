<template>
  <div class="vue-date-container flex">
    <!-- 输入框 -->
    <input type="text" @click="show">
    <!-- 主体 -->
    <div class="main">
      <div class="top">
        <!-- 年份选择 -->
        <div class="left"></div>
        <!-- 月份选择 -->
        <div class="right"></div>
      </div>

      <!-- 日期选择 -->
      <div class="middle">
        <span v-for="day in days">{{ day }}</span>
      </div>

      <div class="bottom">
        <!-- 准确时间 -->
        <div class="time"></div>
        <!-- 操作按钮 -->
        <div class="tool-bar" @click="cancel">取消</div>
        <div class="tool-bar" @click="ok">确定</div>
      </div>
    </div>
  </div>
</template>

<script>
  import _ from 'underscore'

  const defaultOptions = {
  }

  let util = {
    initDate () {
      const dateNow = new Date()
      return {
        year: dateNow.getFullYear(),
        month: dateNow.getMonth() + 1,
        day: dateNow.getDate(),
        hours: dateNow.getHours(),
        mintues: dateNow.getMinutes(),
        seconds: dateNow.getSeconds()
      }
    }
  }

  export default {
    props: ['options'],
    data () {
      return {
        opts: _.extend({}, this.options, defaultOptions)    // configrations
        // 当前显示的时间
        current: {
          year: '',
          month: '',
          day: ''
          hours: '',
          mintues: '',
          seconds: ''
        }
      }
    },

    methods: {
      /**
       * 显示
       */
      show () {
      },
      /**
       * 隐藏
       */
      hide () {},
      /**
       * 确认按钮
       */
      ok () {},

      /**
       * 取消按钮
       */
      cancel () {}
    }
  }

</script>

<style lang="sass" scoped></style>