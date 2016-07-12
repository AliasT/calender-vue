<template>
  <div class="vue-date-container">
    <!-- 输入框 -->
    <input type="text" @click="show">
    <!-- 主体 -->
    <div class="main">
      <div class="top clearfix">
        <!-- 年份选择 -->
        <div class="left">
          <span @click="updateYear(-1)">&lt;&lt;</span>
          <input class="" type="text" v-model="current.year">
          <span @click="updateYear(1)">&gt;&gt;</span>
        </div>
        <!-- 月份选择 -->
        <div class="right">
          <span @click="updateMonth(-1)">&lt;</span>
          <input class="" type="text" v-model="month">
          <span @click="updateMonth(1)">&gt;</span>
        </div>
      </div>
      <div class="weekdays">
        <span class="cell" v-for="(index, weekday) in current.weekdays" track-by="$index">{{weekday}}</span>
      </div>
      <!-- 日期选择 -->
      <div class="middle clearfix">
        <span class="cell" v-bind:style="{ width: start * 30 + 'px' }"></span>
        <span class="cell" v-for="i in days" track-by="$index">{{i+1}}</span>
      </div>

      <div class="bottom clearfix">
        <!-- 准确时间 -->
        <div class="time left"></div>
        <!-- 操作按钮 -->
        <div class="op right">
          <span class="tool-bar" @click="cancel">取消</span>
          <span class="tool-bar" @click="ok">确定</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import _ from 'underscore'
  import util from './util'

  const defaultOptions = {
  }

  export default {
    props: ['options'],
    data () {
      return {
        opts: _.extend({}, this.options, defaultOptions),    // configrations
        // 当前显示的时间
        current: {
          weekdays: [],
          year: 0,
          month: 0,
          day: 0,
          hours: 0,
          mintues: 0,
          seconds: 0,
          days: 0
        },
        days: 0,
        month: 0,
        start: 0
      }
    },

    created () {
      this.current = util.initDate(this.opts)
      this.days = this.current.days
      this.month = this.current.month + 1
    },

    computed: {
      days () {
        return util.getDays(this.current.year)[this.current.month]
      },
      start () {
        var date = new Date()
        date.setFullYear(this.current.year)
        date.setMonth(this.current.month)
        date.setDate(1)
        return date.getDay()
      }
    },

    methods: {
      /**
       * 更改年份
       * @param{number} op 表示增加和减少
       */
      updateYear (op) {
        this.current.year += op
      },

      /**
       * 更改月份
       * @param{number} op 表示增加和减少
       */
      updateMonth (op) {
        this.current.month += op
        this.current.month = this.current.month % 12
        this.month = this.current.month + 1
      },
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

<style lang="sass" scoped>
  .left {
    float: left;
  }

  .right {
    float: right;
  }

  .clearfix:after {
    content: ' ';
    display: block;
    clear: both;
  }

  .flex {
    display: flex;
    &.flex-item-1 {
      display: inline-flex;
    }
    .flex-item-1 {
      flex: 1;
    }
  }

  .top {
    .left, .right {
      text-align: center;
      box-sizing: border-box;
      input {
        text-align: center;
      }
      span {
        font-size: 12px;
        cursor: pointer;
      }
    }
    .left {
      width: 130px;
      input {
        width: 70px;
      }
    }
    .right {
      width: 80px;
      input {
        width: 30px;
      }
    }
  }
  .main {
    width: 210px;
    border: solid 1px #ccc;
    padding: 10px 12px;
  }
  .cell {
    vertical-align: middle;
    text-align: center;
    width: 30px;
    height: 30px;
    box-sizing: border-box;
    float: left;
    line-height: 30px;
  }

  .middle {
    height: 210px;
    .cell:hover {
      background: #eee;
    }
  }
</style>