<template>
  <div class="hello">
  <el-input v-model="input" placeholder="请输入用餐人数"></el-input>
  <el-table :data="list" style="width: 100%">
    <!-- <el-table-column label="id"  >
      <template slot-scope="scope">
       <p>{{scope.row.id}}</p>
      </template>
    </el-table-column> -->
    <el-table-column label="菜名" >
      <template slot-scope="scope">
        <p> {{ scope.row.name }}</p>
      </template>
    </el-table-column>
    <el-table-column label="价格" >
      <template slot-scope="scope">
       <p>{{scope.row.price}}</p>
      </template>
    </el-table-column>
    <el-table-column label="类型"  >
      <template slot-scope="scope">
       <p>{{scope.row.type/1 == 0 ? '大荤': scope.row.type/1 == 1 ? '小荤': scope.row.type/1 == 2 ? '素菜': '汤'}}</p>
      </template>
    </el-table-column>
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button  size="mini"  type="danger"  @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>

  <p>共计消费：{{totalPrice}}，人均消费：{{ input ? totalPrice/(input / 1) : totalPrice}}</p>
      <el-button class='five' type="warning" round  @click="fiveList">随机五个菜</el-button>
      <el-button class='' type="warning" round  @click="clear">一键删除</el-button>
      <el-button type="primary" round @click="type0">随机一个大荤</el-button>
      <el-button type="primary" round @click="type1">随机一个小荤</el-button>
      <el-button type="primary" round @click="type2">随机一个素菜</el-button>
      <el-button type="primary" round @click="type3">随机一个汤类</el-button>
      <!-- <el-button type="primary" round @click="type4">随机一个type4</el-button> -->
      <el-button type="primary" round  @click="one">随机一个菜</el-button>

  </div>
</template>

<script>
import json from '../ft_food.json'
import $ from 'jquery'
export default {
  name: 'HelloWorld',
  data () {
    return {
      json:json.RECORDS,
      list:[],
      input:''
    }
  },
  methods: {
    fiveList(e){
      for(let i = 0; i < 5; i++){
        this.one()
      }
    },
    //随机一个热菜
    type0(){
      var arr = this.common(0)
      $('.five').attr("disabled",true)
      var index  = Math.floor(Math.random() * arr.length)
      this.list.push(arr.splice(index,1)[0])

    },
     type1(){
      var arr = this.common(1)
       $('.five').attr("disabled",true)
      var index  = Math.floor(Math.random() * arr.length)
      this.list.push(arr.splice(index,1)[0])
    },
     type2(){
      var arr = this.common(2)
       $('.five').attr("disabled",true)
      var index  = Math.floor(Math.random() * arr.length)
      this.list.push(arr.splice(index,1)[0])
    },
     type3(){
      var arr = this.common(3)
       $('.five').attr("disabled",true)
      var index  = Math.floor(Math.random() * arr.length)
      this.list.push(arr.splice(index,1)[0])
    },
     type4(){
      var arr = this.common(4)
      $('.five').attr("disabled",true)
      var index  = Math.floor(Math.random() * arr.length)
      this.list.push(arr.splice(index,1)[0])
    },
    clear(){
      for(let i = 0; i < this.list.length;i++){
        this.json.push(this.list[i]);
      }
      //this.json.concat(this.list)
      //console.log(this.json.length)
      this.list = []
      $('.five').removeAttr('disabled')
    },
    //随机一个凉菜
    onecool(){

    },
    //随机一个汤
    onesour(){},
    //随机一个菜
    one(){
      //console.log(arguments)
      $('.five').attr("disabled",true)
      var index  = Math.floor(Math.random() * this.json.length)
      this.list.push(this.json.splice(index,1)[0])
    },
    //common
    common(type){
       $('.five').attr("disabled",true)
      let total = [];
      for(let i = 0; i < this.json.length;i++){

        if(this.json[i].type / 1 == type){
         // console.log(this.json[i].type)
          total.push(this.json[i])
        }
      }
      return total
    },
    //
    handleDelete(index, row) {
        console.log(index, row);
        this.json.push(this.list.splice(index,1)[0]);
        if(!this.list.length){
          $('.five').removeAttr('disabled')
        }
      }
  },
  computed:{
    totalPrice:function(){
      console.log(this)
      let total = 0;
      for (let i in this.list) {
        total += this.list[i].price / 1;
      }
      return total;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  scoped>
  .hello{
    width:100%;
  }
  button{
    width: 100%;
    margin: 10px 0px !important;
  }

</style>
<style>
  .cell {
    text-align: center;
}
</style>


