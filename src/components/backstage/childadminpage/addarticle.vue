<template>
  <div id='edit'>
    <div class="article-left">
      <h2>撰写新文章</h2>
      <div><input type='text' placeholder="请在此处输入文章标题" v-model="title"></div>
      <div><input type='text' placeholder="作者" v-model="author"></div>
      <div><input type='date' placeholder="时间" v-model="time"></div>
  
 <div class="adminstration-right toolbar" id='editor' ></div>
 
          </div>
          <div class="article-right-aside">
<div class="col-md-3">
           
            <div class="add-article-box">
              <h2 class="add-article-box-title"><span>标签</span></h2>
              <div class="add-article-box-content">
                <input type="text" class="form-control" placeholder="输入新标签"  v-model="tag" >
                <span class="prompt-text">多个标签请用英文逗号,隔开</span> </div>
            </div>
                <div class="add-article-box">
              <h2 class="add-article-box-title"><span>栏目</span></h2>
              <div class="add-article-box-content">
               <select @change="choosecolumn($event)"><option >技术</option><option class="column">个人</option></select>
                </div>
            </div>
            <div class="add-article-box">
              <h2 class="add-article-box-title"><span>标题图片</span></h2>
              <div class="img-view"><img :src='head_img' alt='缩略图片预览'></div>
              <div class="add-article-box-content">
                <input type="file" class="form-control" ref='thumb' id="pictureUpload" @change="ViewImg($event)" >
              </div>
             
            </div>
            <div class="add-article-box">
              <h2 class="add-article-box-title"><span>发布</span></h2>
              <div class="add-article-box-content">
              	<p><label>状态：</label><span class="article-status-display">未发布</span></p>
                <p><label>公开度：</label><input type="radio" name="visibility" value="0" checked/>公开 <input type="radio" name="visibility" value="1" />加密</p>
                <p><label>发布于：</label><span class="article-time-display"><input style="border: none;" type="datetime" name="time" value="2016-01-09 17:29:37" /></span></p>
              </div>
              <div class="add-article-box-footer">
                <button class="btn btn-primary" type="submit" name="submit" @click="showd">发布</button>
              </div>
            </div>
          </div>
          </div>
  </div>
</template>
<script>
import edit from "@/components/backstage/childadminpage/edit";
export default {
  components: {
    edit
  },
  data() {
    return {
      column:'',
      thumbnail:'',
      title: "",
      author: "",
      time: "",
      head_img: "",
      imgsrc:'',
      tag:'',
      imgFile:{}
    };
  },
  methods: {
    showd() {
      // this.$refs.thumb.click()
      //      console.log(this.titlemessage,this.authormessage,this.timemessage)
      // console.log(this.edit.txt.html())
     
 var formdata = new FormData();

      formdata.append("uploadarticleimg",  this.imgFile);
      let config = { headers: { "Content-Type": "multipart/form-data" } };
      this.$http
        .post("api/articleimg", formdata, config)
        .then(res => {
          this.thumbnail=res.data.newPath;
          console.log(res.data.newPath);
      this.$http.post("api/createarticle", {
        column:this.column,
        thumbnail:this.thumbnail,
        tag:this.tag,
        picsrc: this.imgsrc,
        title: this.title,
        author: this.author,
        time: this.time.replace(/\-/g, "/"),
        article: this.edit.txt.html()
      }).then(res=>{
        console.log(res);
        if(res.status==200){
          alert('文章添加成功')
        }
      });


        });

    },
    ViewImg(e) {
      this.imgFile=e.target.files[0];
      var newfile = new FileReader();
      newfile.readAsDataURL(e.target.files[0]);
      var that = this;
      newfile.onload = function() {
        that.head_img = this.result;
      };
      
    },
    choosecolumn(e) {
      this.column=e.target.value;
      console.log((e.target.value = "个人"));
    }
  },
  mounted() {
    var E = require("wangeditor");
    // var E = window.wangEditor
    var editor = new E("#editor");

    editor.customConfig.uploadImgServer =
      `/api/articleimg`; //上传URL

    editor.customConfig.uploadFileName = "uploadarticleimg";

    // editor.customConfig.linkImgCallback = function (url) {
    //     console.log(url) // url 即插入图片的地址,,插入网络图片时，可通过如下配置获取到图片的信息
    // }
    var that = this;

    editor.customConfig.uploadImgHooks = {
      success: function(xhr, editor, result) {
        // 图片上传并返回结果，图片插入成功之后触发
        // xhr 是 XMLHttpRequst 对象，editor 是编辑器对象，result 是服务器端返回的结果
        that.imgsrc =  `/articleimg/${result.imgname}`;
      },
      customInsert: function(insertImg, result, editor) {
        // 图片上传并返回结果，自定义插入图片的事件（而不是编辑器自动插入图片！！！）
        // insertImg 是插入图片的函数，editor 是编辑器对象，result 是服务器端返回的结果

        var url =  `/articleimg/` + result.imgname;
        insertImg(url);
        // result 必须是一个 JSON 格式字符串！！！否则报错
      }
    };
    editor.create();

    this.edit = editor;
  }
};
</script>
<style scoped>
.article-left {
  width: 70%;
  float: left;
}
.article-right-aside {
  width: 30%;
  float: left;
}
input {
  color: #666;
  background-color: transparent;
  border: none;
  border: 1px solid #ccc;
  box-shadow: 0px 0px 8px rgb(107, 214, 205);
}

input:focus {
  border: 1px solid rgb(214, 107, 107);
  box-shadow: 0px 0px 8px rgb(214, 107, 107) inset 0px 0px 8px
    rgb(214, 107, 107);
}
.img-view {
  height: 150px;
  width: 200px;
  margin-bottom: 20px;
}
.img-view img {
  /* width: 100%;
  height: 100%; */
}
</style>


