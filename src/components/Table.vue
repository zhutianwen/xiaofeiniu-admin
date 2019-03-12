<template>
   <div class="xfn-table-info">
      <el-card shadow="hover">
        <div class="xfn-table" :style="{background:getTableColor(data.status)}">{{data.tid}}号桌:{{data.status|tableStatus}}</div>
        <el-button type="primary" round size="mini" @click="showTableDetail">详情</el-button>
        <el-button type="warning" round size="mini">修改</el-button>
      </el-card>

      <!--桌台详情对话框-->
      <el-dialog :title="data.tid+'号桌台详情'" :visible="dialogTableDetailVisible" :before-close="closeDialogTableDetail">
      <!--对话框主体-->
         <el-tabs type="border-card" @tab-click="makeQRCode">
           <el-tab-pane label="桌台详情">详情</el-tab-pane>
           <el-tab-pane label="桌台二维码">
          <img :src="qrcodeData">
           </el-tab-pane>
         </el-tabs> 
      <!--对话框尾部--> 
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
         qrcodeData:''  
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
      },
      closeDialogTableDetail(){
          this.dialogTableDetailVisible=false;
      },
      makeQRCode(){
          //创建二维码--注意此方法不能再当前组件的mounted中调用，因为绘图必需的canvas在el-dialog中 对话框在组件加载时并不在dom树上
          var qrcode=require('qrcode');
          var tableUrl=this.$store.state.globalSettings.appUrl+'/#/'+this.data.tid;
          //把绘制得到的图片二进制转换为字符编码
          qrcode.toDataURL(tableUrl,{width:300,errorCorrectionLevel:'H'},(err,url)=>{
             this.qrcodeData=url;  
          })
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