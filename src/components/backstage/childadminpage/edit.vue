<template>
<div>
  <input type='submit' @click="showd" >
  <div class="adminstration-right toolbar" id='editor' ></div>

  </div>
</template>
<script>

export default {
  data(){
    return{
imgsrc:'',
netHref:''
    }
  },
  props:[
    'titlemessage','authormessage','timemessage'
  ],
  methods:{
   showd(){
//      console.log(this.titlemessage,this.authormessage,this.timemessage)
// console.log(this.edit.txt.html())

this.$http.post('api/createarticle',{
  
 picsrc:this.imgsrc, 
title:this.titlemessage,
author:this.authormessage,
time:this.timemessage.replace(/\-/g,'/'),
article:this.edit.txt.html()
})
   } 
  },
mounted(){
 console.log(this.netHref+'555555555')
  var E=require('wangeditor')
  // var E = window.wangEditor
var editor= new E('#editor');

   
editor.customConfig.uploadImgServer = `/api/articleimg`; //上传URL
   
editor.customConfig.uploadFileName = 'uploadarticleimg';

// editor.customConfig.linkImgCallback = function (url) {
//     console.log(url) // url 即插入图片的地址,,插入网络图片时，可通过如下配置获取到图片的信息
// }
var that=this;

editor.customConfig.uploadImgHooks = {

  success: function (xhr, editor, result) {
        // 图片上传并返回结果，图片插入成功之后触发
        // xhr 是 XMLHttpRequst 对象，editor 是编辑器对象，result 是服务器端返回的结果
        that.imgsrc= `/articleimg/${result.imgname}`

    },
    customInsert: function (insertImg, result, editor) {
                // 图片上传并返回结果，自定义插入图片的事件（而不是编辑器自动插入图片！！！）
                // insertImg 是插入图片的函数，editor 是编辑器对象，result 是服务器端返回的结果
         
                var url = `/articleimg/${result.imgname}`;
        insertImg(url)
                // result 必须是一个 JSON 格式字符串！！！否则报错
            }
        }
        editor.create();

this.edit=editor;

}
}
</script>

<style scoped>
.adminstration-right{

  width:100%;
  /* margin-left:210px; */
 
padding-top:50px;
}
</style>
