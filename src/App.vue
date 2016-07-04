<template>
  <div id="app">
    <Vuedate :options="options"></Vuedate>
  </div>
</template>

<script>
  import Vuedate from 'components/date'

  export default {
    components: { Vuedate },
    data () {
      return {
        // 选项
        options: {
          skin: 'blue'
        }
      }
    }
  }
</script>

<style lang="sass"></style>