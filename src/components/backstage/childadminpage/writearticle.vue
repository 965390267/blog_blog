<template>
  <div class="adminstration-right toolbar" >
    <div class="adminstration-add" v-if='isshow'>
      <h2>操作</h2>
      <div @click="addarticle"  class="addarticle"><router-link to='/adminstration/writearticle/addarticle' >增加文章</router-link></div>
      <h2>管理</h2>
      <div>
        <ul class="article">
          <li class="article-li "><ul class="article-li-one"><li>选择</li><li>标题</li>
          <li>栏目</li>
          <li>标签</li><li>评论</li><li>日期</li><li>操作</li></ul></li>
          <li class="article-li " v-for='(item,index) in article' :key='index'>
            <ul class="article-li-one">
              <li><input type='checkbox'  @change="checked($event)"></li>
              <li>{{item.title}}</li>
              <li>{{item.column}}</li>
              <li>{{item.tag}}</li>
              <li>5</li>
              <li>{{item.time}}</li>
              <li><i  @click="addarticle"><router-link  to='/adminstration/writearticle/addarticle' >修改</router-link></i><a @click="deleteart(index)">删除</a></li>
              </ul>
              </li>
      
         
        </ul>
      </div>
      <div>
        <ul><li><<</li><li>1</li><li>2</li><li>>></li></ul>
      </div>
      <div><span>全选</span><span>反选</span><span>不选</span><span>删除</span></div>
      </div>
<router-view class="addarticle-view"></router-view>
  </div>
</template>
<script>
export default {
  data(){
    return{
      article:[],
isshow:true,
articleId:''

    }
  },
  methods:{
addarticle(){
  this.isshow=false
},
getArtMes(){
  this.$http.get('api/getarticle').then(res=>{
    this.article=res.data
  
  })
},
checked(e){
  console.log(e.target.checked)
},
deleteart(i){
 var res=  confirm('确定删除该篇文章吗？')
console.log()
if(res){
this.articleId= this.article[i]._id;

this.$http.post('api/deletearticle',{artid:this.articleId}).then((res)=>{
  console.log(res.data.deleteart);
  if(res.data.deleteart=='ok'){
    alert('删除成功')
  }
  this.getArtMes()
})
}else{
  alert('取消删除')
}

},
choosecolumn(e,i){
console.log(e.target.value,i)
}
  },
  mounted(){
this.getArtMes()
  }
};
</script>

<style scoped>
.adminstration-add{
  width: 95%;
}
.adminstration-right {
  width: 100%;
  margin-left: 210px;
  padding-top: 100px;
}
.article-li{
 padding: 20px;
}
.article-li-one li{
  text-align: center;
   width: 14.1%;
 display: inline-block;

}
.article-li-one li:nth-child(1){
   width: 8%;
 display: inline-block;
}
.addarticle-view{
  position: absolute;
  top: 0px;
  left:0px;
  width: 100%;
    margin-left: 210px;
    padding-top: 100px;
}
</style>
