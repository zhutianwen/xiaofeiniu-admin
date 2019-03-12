<template>
  <div class="xfn-category-list">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">首页</el-breadcrumb-item>
      <el-breadcrumb-item>菜品类别管理</el-breadcrumb-item>
      <el-breadcrumb-item>类别列表</el-breadcrumb-item>
    </el-breadcrumb>
     <br>
    <el-button type="primary" size="mini" @click="add">
    添加新的菜品类别
    </el-button>
      <br>
    <el-table :data="categoryList" stripe border>
       <el-table-column label="编号" prop="cid"></el-table-column>
       <el-table-column label="名称" prop="cname"></el-table-column>
      
       <el-table-column label="操作" >
         <template slot-scope="{row,$index}">
             <el-button @click="updateCategory(row,$index)" type="success" size="mini">修改</el-button>
             <el-button @click="deleteCategory(row,$index)" type="danger" size="mini">删除</el-button>
         </template>
          
       </el-table-column>
    </el-table>
  </div>
</template>

<script>
  export default{
    data(){
      return{
        categoryList:[]
      }
    },
    methods:{ 
      deleteCategory(c,i){
        this.$confirm("操作不可撤销 确定",'提示',{type:"warning"}).then(()=>{
            var url=this.$store.state.globalSettings.apiUrl+'/admin/category/'+c.cid;
        this.$axios.delete(url).then((res)=>{
           if(res.data.code==200){//数据库中删除成功
             this.categoryList.splice(i,1);//从模型数据库中删除
             this.$message.success('删除成功');
           }else{
             this.$message.error('删除失败:'+res.data.msg)
           } 
        }).catch((err)=>{
          console.log(err);
        })
        }).catch(()=>{

        })
        
      },
      updateCategory(c,i){
          console.log(c);
        console.log(i);
      },
      addCategory(){
        this.$prompt('请输入新的菜品类别名:','提示',{type:'info'}).then((result)=>{
           console.log(reult);
        }).catch(()=>{
        })
      }
    },
  mounted(){
    var url=this.$store.state.globalSettings.apiUrl+'/admin/category';
    this.$axios.get(url).then((res)=>{
        this.categoryList=res.data;
    }).catch((err)=>{
      console.log(err)
    })
  },
  }
</script>