<template>
  <div class="content-wrapper">
    <div class="flash-container flash-container-page">
    </div>
    <div class="container-fluid container-limited ">
      <div class="content">
        <c-new></c-new>
      </div>
    </div>
  </div>
</template>

<style lang="styl" rel="stylesheet/stylus" scoped type="text/css">
  .headIcon
    width 150px
    height 150px
    border-radius 50%
    overflow hidden
    margin 20px
    img
      width: 100%
      height 100%
</style>

<script type="text/ecmascript-6">
  import BasePage from 'src/extend/BasePage'
  import CNew from './CNew.vue'
  export default{
    mixins: [ BasePage ],
    components: { CNew },
    name: 'groups_new',
    data () {
      return {
        // 一个典型列表数据格式
        options: [ {
          value: '1',
          label: 'H5deplov'
        }, {
          value: '2',
          label: 'Util'
        }, {
          value: '2',
          label: '添加新组'
        } ],
        value: '',
        // 一个典型列表数据格式
        form: {
          image: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100',
          name: '',
          groupId: '',
          description: ''
        }
      }
    },
    mounted: function () {
    },
    methods: {
      onSubmit: function () {

      }
    }
  }
</script>
