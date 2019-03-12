<template>
   <div class="xfn-table-info">
      <el-card shadow="hover">
        <div class="xfn-table" :style="{background:getTableColor(data.status)}">{{data.tid}}号桌:{{data.status|tableStatus}}</div>
        <el-button type="primary" round size="mini" @click="showTableDetail">详情</el-button>
        <el-button type="warning" round size="mini">修改</el-button>
      </el-card>

      <!--桌台详情对话框-->
      <el-dialog :title="data.tid+'号桌台详情'" :visible="dialogTableDetailVisible">
        <div slot="footer">
           <el-button type="primary" @click="dialogTableDetailVisible=false">确定</el-button>
        </div>
      </el-dialog>
   </div>
</template>

<script>
export default {
    data(){
       return{
         dialogTableDetailVisible:false,  
       } 
    },
  props:['data'],
  methods: {
      getTableColor(status){
          if(status==1) return '#67C23A';
          else if(status==2) return '#E6A23C';
          else if(status==3) return '#F56C6C';
          else return '#909399';
      },
      showTableDetail(){
      //console.log(this.data) 当前桌子的数据
      this.dialogTableDetailVisible=true
      } 
  },  
  
}
</script>

<style lang="scss">
    .xfn-table-info{
       padding:3px;
       text-align:center;

      .xfn-table{
          width:95%;
          height:150px;
          line-height:150px;
          border:1px solid #aaa;
          border-radius:10%;
          box-shadow:-4px -6px 5px #666;  
          margin:8px auto;
      } 
    }
</style>