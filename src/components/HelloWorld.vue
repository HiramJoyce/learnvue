<template>
  <div class="hello">
    <hr>
    <el-upload
      class="upload-demo"
      action="http://localhost:8888/upload/img"
      :on-preview="handlePreview"
      :on-remove="handleRemove"
      :before-remove="beforeRemove"
      multiple
      :onError="uploadError"
      :onSuccess="uploadSuccess"
      :limit="3"
      :on-exceed="handleExceed"
      :file-list="fileList">
      <el-button size="small" type="primary">点击上传</el-button>
      <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
    </el-upload>
    <hr>
    <el-upload
      class="upload-demo"
      action="http://localhost:8888/upload/img"
      :on-preview="handlePreview"
      :on-remove="handleRemove"
      :onSuccess="uploadSuccess"
      :file-list="fileList2"
      list-type="picture">
      <el-button size="small" type="primary">点击上传</el-button>
      <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
    </el-upload>
    <hr>
    <span>照片墙</span>
    <el-upload
      action="http://localhost:8888/upload/img"
      list-type="picture-card"
      :on-preview="handlePictureCardPreview"
      :on-remove="handleRemove"
      :before-remove="beforeRemove">
      <i class="el-icon-plus"></i>
    </el-upload>
    <el-dialog :visible.sync="dialogVisible">
      <img width="100%" :src="dialogImageUrl" alt="">
    </el-dialog>
    <hr>
    <span>头像</span>
    <div id="pick-avatar" @mouseenter="editHeadImg(1)" @mouseleave="editHeadImg(2)" style="position:relative; clear: both;">
      <img src="./../assets/34761f13f85549f0.jpg" style="position:absolute; height: 50px; width: 50px; border-radius: 25px;"/>
      <div v-if="editImg" style="position:absolute; margin-top: 25px; height: 25px; width: 50px; border-bottom-left-radius: 25px; border-bottom-right-radius: 25px; background-color: rgba(0,0,0,0.5); line-height: 25px; text-align: center;"><i class="el-icon-edit" style="color: cornsilk"></i></div>
    </div>
    <avatar-cropper
      @uploaded="handleUploaded"
      trigger="#pick-avatar"
      upload-url="http://localhost:8888/upload/img" />
  </div>
</template>

<script>
import AvatarCropper from 'vue-avatar-cropper'
export default {
  name: 'HelloWorld',
  components: { AvatarCropper },
  data () {
    return {
      // userAvatar: undefined, //用户头像地址
      dialogImageUrl: '',
      dialogVisible: false,
      editImg: false,
      fileList: [{name: 'food.jpeg', url: 'http://localhost:8081/static/img/34761f13f85549f0.84c47bc.jpg'}, {name: 'food2.jpeg', url: 'http://localhost:8081/static/img/34761f13f85549f0.84c47bc.jpg'}],
      fileList2: [{name: 'food.jpeg', url: 'http://localhost:8081/static/img/34761f13f85549f0.84c47bc.jpg'}, {name: 'food2.jpeg', url: 'http://localhost:8081/static/img/34761f13f85549f0.84c47bc.jpg'}]
    }
  },
  methods: {
    editHeadImg (n) {
      this.editImg = n === 1
    },
    handleUploaded (resp) {
      // this.userAvatar = resp.relative_url
      console.log(resp)
    },
    handleRemove (file, fileList) {
      console.log(file, fileList)
    },
    handlePreview (file) {
      console.log(file)
    },
    handleExceed (files, fileList) {
      this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`)
    },
    beforeRemove (file, fileList) {
      return this.$confirm(`确定移除 ${file} ？` + fileList)
    },
    uploadSuccess (response, file, fileList) {
      console.log('上传文件' + response + file + fileList)
    },
    uploadError (response, file, fileList) {
      console.log('上传失败，请重试！' + response + file + fileList)
    },
    handlePictureCardPreview (file) {
      this.dialogImageUrl = file.url
      this.dialogVisible = true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
