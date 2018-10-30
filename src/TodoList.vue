<template>
  <div>
    <Header></Header>
    <div align="center">
      <el-input v-model="inputValue" placeholder="接下去要做什么？" style="width: 500px;">
        <el-button slot="append" icon="el-icon-edit" @click="handleSubmit"></el-button>
      </el-input>
    </div>
    <el-row :gutter="20">
      <el-col :span="9"  :offset="3">
        <el-card class="box-card" style="margin-top: 10px" >
          <div slot="header" class="clearfix">
            <span>待完成</span>
            <el-button style="float: right; padding: 3px 0" type="text" @click="clearList">清空</el-button>
          </div>
          <div v-for="(o,index) in list" :key="o" class="text item">
            {{''+o }}
            <el-button-group style="float: right">
              <el-button size="small" type="success" icon="el-icon-check" circle @click="handleFinish(o,index)"></el-button>
              <el-button size="small" type="danger" icon="el-icon-delete" circle  @click="handleDelete(index)"></el-button>
            </el-button-group>
          </div>
        </el-card>
      </el-col>
      <el-col :span="9">
        <el-card class="box-card" style="margin-top: 10px" >
          <div slot="header" class="clearfix">
            <span>已完成</span>
            <el-button style="float: right; padding: 3px 0" type="text" @click="clearFinish">清空</el-button>
          </div>
          <div v-for="(o,index) in finishList" :key="o" class="text item">
            {{''+o }}
            <el-button-group style="float: right">
              <el-button size="small" type="warning" icon="el-icon-back" circle @click="handleBack(o,index)"></el-button>
              <el-button size="small" type="danger" icon="el-icon-delete" circle  @click="handleDelete_finish(index)"></el-button>
            </el-button-group>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>
<script>
  import Header from './todo/header'
  export default {
    components:{
      Header,
    },
    data(){
      return{
        inputValue: '',
        list:[],
        finishList:[]
      }
    },
    methods:{
      handleSubmit(){
        if(this.inputValue === ''){
          this.$notify({
            title: '失败',
            message:'输入值不能为空',
            type: 'error',
            duration: 2000
          });
        }else {
          this.list.push(this.inputValue);
          this.inputValue = '';
        }
      },
      handleFinish(item,index){
        this.finishList.push(item);
        this.handleDelete(index);
      },
      handleDelete(index){
        this.list.splice(index,1);
      },
      handleDelete_finish(index){
        this.finishList.splice(index,1);
      },
      handleBack(item,index){
        this.list.push(item);
        this.handleDelete_finish(index);
      },
      clearList(){
        this.list =[];
      },
      clearFinish(){
        this.finishList =[];
      }
    }

  }
</script>

<style>
  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 18px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }

  .box-card {
    width: 480px;
  }
</style>
