<template>
  <div class="weiyu-right">
      <div class="col-sm-9 col-sm-offset-3 col-md-10 col-lg-10 col-md-offset-2 main" id="main">
      <form action="/Comment/checkAll" method="post">
        <h1 class="page-header">管理 <span class="badge">4</span></h1>
        <div class="table-responsive">
          <table class="table table-striped table-hover">
            <thead>
              <tr>
                <th><span class="glyphicon glyphicon-th-large"></span> <span class="visible-lg">选择</span></th>
                <th><span class="glyphicon glyphicon-file"></span> <span class="visible-lg">摘要</span></th>
                <th><span class="glyphicon glyphicon-time"></span> <span class="visible-lg">日期</span></th>
                <th><span class="glyphicon glyphicon-pencil"></span> <span class="visible-lg">操作</span></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for='(item,index) in weiyu' :key='index'>
                <td><input type="checkbox" class="input-control" name="checkbox[]" value="" /></td>
                <td class="article-title">{{item.weiyu}}</td>
                <td>{{item.time}}</td>
                <td><a rel="1" name="see">查看</a> <a rel="1" name="delete" @click="deleteweiyu(index)">删除</a></td>
              </tr>
             
            </tbody>
          </table>
        </div>
        <footer class="message_footer">
          <nav>
            <div class="btn-toolbar operation" role="toolbar">
              <div class="btn-group" role="group"> <a class="btn btn-default" onClick="select()">全选</a> <a class="btn btn-default" onClick="reverse()">反选</a> <a class="btn btn-default" onClick="noselect()">不选</a> </div>
              <div class="btn-group" role="group">
                <button type="submit" class="btn btn-default" data-toggle="tooltip" data-placement="bottom" title="删除全部选中" name="checkbox_delete">删除</button>
              </div>
            </div>
            <ul class="pagination pagenav">
              <li class="disabled"><a aria-label="Previous"> <span aria-hidden="true">&laquo;</span> </a> </li>
              <li class="active"><a>1</a></li>
              <li class="disabled"><a aria-label="Next"> <span aria-hidden="true">&raquo;</span> </a> </li>
            </ul>
          </nav>
        </footer>
      </form>
    </div>
          <div class="add-article-box">
              <h2 class="add-article-box-title"><span>微语图片</span></h2>
              <div class="img-view"><img :src='head_img' alt='缩略图片预览'></div>
              <div class="add-article-box-content">
                <input type="file" class="form-control" ref='thumb' id="pictureUpload" @change="ViewImg($event)" >
              </div>
             
            </div>
        <div><input type='text' placeholder="请输入微语" v-model="weiyutxt"></div>
      
      <div><input type='date' placeholder="时间" v-model="time"></div>
      <div @click="btn">提交</div>
  </div>
</template>
<script>
export default {
    data(){
        return{
 weiyutxt:'',
weiyu:'',
time:'',
head_img:'',
imgFile:{},
weiyuId:''
        }
    },
    methods:{
        getweiyu(){
            this.$http.get('api/getweiyu').then(res=>{
                console.log()
                this.weiyu=res.data
            })
        },
        deleteweiyu(i){
 var res=  confirm('确定删除该微语吗？')
console.log()
if(res){
this.weiyuId= this.weiyu[i]._id;

this.$http.post('api/deleteweiyu',{weiyuid:this.weiyuId}).then((res)=>{
  console.log(res.data.deleteweiyu);
  if(res.data.deleteweiyu=='ok'){
    alert('删除成功')
  }
  this.getweiyu();//删除完成后重新获取微语
})
}else{
  alert('取消删除')
}

},
   btn(){
//      console.log(this.titlemessage,this.authormessage,this.timemessage)
// console.log(this.edit.txt.html())
var formdata = new FormData();

      formdata.append("upweiyuimg",  this.imgFile);
      let config = { headers: { "Content-Type": "multipart/form-data" } };
      this.$http
        .post("api/weiyuimg", formdata, config).then(res=>{
            console.log(res.data.newPath)
            this.$http.post('api/postweiyu',{weiyu:this.weiyutxt,time:this.time,headimg:res.data.newPath})
        })

   },
    ViewImg(e) {
      this.imgFile=e.target.files[0];
      var newfile = new FileReader();
      newfile.readAsDataURL(e.target.files[0]);
      var that = this;
      newfile.onload = function() {
        that.head_img = this.result;
      };
      
    }
    },
    mounted(){
this.getweiyu();
    }
};
</script>
<style scoped>
.weiyu-right{
    margin-left: 200px;
}
.img-view {
  display: inline-block;
  height: 150px;
  width: 200px;

}
.img-view img {
  width: 100%;
  height: 100%;
}
</style>
