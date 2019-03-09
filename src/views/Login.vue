<template>
  <div class="login">
      <el-card class="xfn-login-card">
         <div slot="header">管理员登录</div>
         <div>
           <el-form label-width="80px">

              <el-form-item label="管理员名:">
                 <el-input v-model="formData.aname" placeholder="请输入管理员名"></el-input>
              </el-form-item>

              <el-form-item label="管理密码:">
                 <el-input type="password" v-model="formData.apwd" placeholder="请输入管理员密码"></el-input>
              </el-form-item> 

              <el-form-item @click.native="">
                 <el-button type="primary" @click="doLogin">登录</el-button>
                 <el-button type="" @click="doCancel">取消</el-button>
              </el-form-item>

           </el-form>
         </div>
      </el-card>
      {{$store.state.globalSettings}}
  </div>
</template>

<script>
export default {
   data(){
     return{
       formData:{
         aname:'',
         apwd:''
       }
     }
   },
   methods:{
     doLogin(){ //执行登录
        var url=this.$store.state.globalSettings.apiUrl+`/admin/login/${this.formData.aname}/${this.formData.apwd}`
        this.$axios.get(url).then((res)=>{
          if(res.data.code==200){
            //把用户名存入Vuex仓库
            this.$store.commit('setAdminName',this.formData.aname);
            this.$router.push('/main')
          }else{
            this.$alert("用户名或密码有误","登录失败",{type:"error"})
          }    
        }).catch((err)=>{
           console.log(err);
        })
        //console.log(url);
     },
     doCancel(){// 清除用户的输入
       this.formData.aname='';
       this.formData.apwd='';
     }
   },
}
</script>

<style lang="scss">
  .xfn-login-card{
    width:450px;
    margin:150px auto;
  }
  .xfn-login-card .el-card__header{
   text-align:center; 
   font-size:1.2em;
  }
</style>