<template>
  <div>
    <hr>
    <el-form ref="form" :model="form" label-width="80px">
      <el-form-item label="图标">
        <div class="headIcon">
          <img :src="form.logo">
        </div>
        <upload :on-success="uploadEnd"></upload>
        <div class="el-upload__tip" slot="tip">只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-form-item>

      <el-form-item label="名称">
        <el-input placeholder="名称" v-model="form.name">
        </el-input>
      </el-form-item>
      <el-form-item label="描述">
        <el-input type="textarea" v-model="form.description"></el-input>
      </el-form-item>

      <div class="form-group">
        <div class="col-sm-offset-2 col-sm-10">
          <ul>
            <li>项目都是在每个具体的分组里面</li>
            <li>每个组里面可以添加多个用户，添加的用户都可以看到该组的项目</li>
            <li>项目的名称是和组名一起唯一确定项目的</li>
            <li>分组不能重复</li>
          </ul>

        </div>
      </div>

      <el-form-item>
        <el-button type="primary" @click="onSubmit">立即创建</el-button>
      </el-form-item>

    </el-form>
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
  import Server from 'src/extend/Server'
  import Upload from 'src/components/Upload'
  export default{
    mixins: [ BasePage ],
    components: { Upload },
    name: 'groups_cnew',
    props: { id: '' },
    data () {
      return {
        info: {},
        form: {
          logo: '',
          name: '',
          description: ''
        }
      }
    },
    mounted: function () {
      if (this.id) {
        Server({
          url: 'project/groupinfo',
          method: 'get',
          params: {
            id: this.id
          }
        }).then((response) => {
          this.info = response.data.data
          this.form.logo = this.info.logo
          this.form.name = this.info.name
          this.form.description = this.info.description
        })
      }
    },
    methods: {
      uploadEnd: function (url) {
        this.form.logo = url
      },
      onSubmit: function () {
        if (this.info.id) {
          var req = {
            logo: this.form.logo,
            name: this.form.name,
            description: this.form.description,
            id: this.info.id
          }
          Server({
            url: 'project/group',
            method: 'put',
            data: req
          }).then((response) => {
            this.$message('修改成功')
            if (!this.id) {
              this.$router.push({ path: 'groups_members', query: { id: this.info.id } })
            }
          }).catch(() => {

          })
        } else {
          Server({
            url: 'project/group',
            method: 'post',
            data: this.form
          }).then((response) => {
            this.$message('添加成功')
            this.$router.push({ path: 'dashboard_groups' })
          }).catch(() => {

          })
        }
      }
    }
  }
</script>
