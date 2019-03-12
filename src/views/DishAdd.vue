<template>
  <div class="xfn-dish-add">
     <el-breadcrumb>
       <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
       <el-breadcrumb-item>添加菜品</el-breadcrumb-item>
    </el-breadcrumb>
<br><br>
    <el-form label-width="100px">
       <el-form-item label="菜品图片:">
          <el-upload class="xfn-uploader" :action="uploadAction" :on-success="doUploadSucc" name="dishImg" :show-file-list="false">
             <img v-if="imageUrl" :src="imageUrl">
          </el-upload>
       </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data(){
    return{
      imageUrl:'', //要显示的预览图片地址
      uploadAction:this.$store.state.globalSettings.apiUrl+'/admin/dish/image'  //可处理文件上传的数据API
    }
  },
  methods: {
    doUploadSucc(res,file){
      //文件上传成功后,客户端得到相应消息之后的处理函数
      //res: 服务器端返回的响应消息
      //file:从input[]
      console.log(res);
      this.imageUrl=URL.createObjectURL(file.raw);
      //把上传的文件编码为DataURL字符串
    }
  },
}
</script>

<style lang="scss">
  .xfn-uploader{
    .el-upload{
      border:1px dotted #aaa;
      border-radius:3px;
      cursor:pointer;
      width:250px;
      height:176px;
      overflow:hidden;
      &:hover{
        border-color:blue;
      }
    }
     img{
      max-width:100%;
     }
  }
</style>