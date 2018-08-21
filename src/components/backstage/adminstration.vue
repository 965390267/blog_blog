<template>
  <div id='adminstration'>
<div class="adminstration-head">
<div class="admin-head-left-logo">这儿是logo</div>
<div class="admin-right">
  <div class="admin-search">
  <input type='text' placeholder="查找">
  <!-- <span>查找</span> -->
  <div class="search"><i class="iconfont icon-sousuo"></i></div>
  </div>
  <div class="admin-mes">
    <div class="admin-mes-tip">消息<span class="admin-mes-circle">1</span></div>
    <div class="admin-main-name"><div>admin</div><i>箭头</i></div>
    <div  class="cancel-admin">退出登录</div>
  </div>
</div>
</div>
<div class="admin-content">
<div class="adminstration-left">
  <ul>
    <li  @click='show(0)' :class="{liactive:isactive==0}"><router-link to='/adminstration/allmes'><i class="iconfont icon-yingyongzonglan"></i>信息总览</router-link></li>
    <li @click='show(1)' :class="{liactive:isactive==1}"><router-link to='/adminstration/writearticle'><i class="iconfont icon-wenzhangguanli"></i>文章发布</router-link></li>  
  
    <li @click='show(2)' :class="{liactive:isactive==2}"><router-link to='/adminstration/comment'><i class="iconfont icon-pinglun"></i>评论</router-link></li>
    <li @click='show(3)' :class="{liactive:isactive==3}"><router-link to='/adminstration/leavemessage'><i class="iconfont icon-liuyan"></i>留言</router-link></li>
    <li @click='show(4)' :class="{liactive:isactive==4}"><router-link to='/adminstration/easywrite'><i class="iconfont icon-bi"></i>随笔</router-link></li>
    <li @click='show(5)' :class="{liactive:isactive==5}"><router-link to='/adminstration/photoupload'><i class="iconfont icon-zhaopian"></i>照片上传</router-link></li>
     <li @click='show(6)' :class="{liactive:isactive==6}"><router-link to='/adminstration/musicupload'><i class="iconfont icon-yinle"></i>音乐上传</router-link></li>
    <li @click='show(7)' :class="{liactive:isactive==7}"><router-link to='/adminstration/save'><i class="iconfont icon-shezhi"></i>设置</router-link></li>
  </ul>
</div>
<router-view></router-view>
<!-- <allmes></allmes> -->
  </div>
   
  </div>
  
</template>


<script>
// import edit from "@/components/backstage/childadminpage/edit";
import allmes from "@/components/backstage/childadminpage/allmes";
export default {
  components: {
    // edit,
    allmes
  },
  data(){
    return{
isactive:0,

    }
  },
  methods: {
show(index){

this.isactive=index;
},
checklogin(){
        this.$http
          .post("api/login", {
            params: {
              usename:sessionStorage.getItem('usename'),
              password:sessionStorage.getItem('password')
            }
          })
          .then(response => {     
            if(response.data.pass!='ok'){

                  alert('非法登录');
                   this.$router.push('/admin')
            }
          });
}
  },
  mounted() {

this.checklogin()
 this.$router.push('/adminstration/allmes')

   
  }
};
</script>


<style scoped>
div,li,span{
  font-family: "Segoe Script", 楷体;
      /* font-family: sans-serif; */
}
#adminstration {
  background-image: url("../../assets/images/starsky2.jpg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  background-origin: content-box;
    overflow: auto;
}
.adminstration-head {
  height: 60px;
  margin-top: 10px;
  margin-bottom: 10px;
}
.admin-head-left-logo {
  float: left;
}
.admin-right {
  float: right;
}
.admin-right .search{
  position: absolute;
  top:1px;
  right:3px;
}
.admin-right .search:hover{
 cursor: pointer;
}
.admin-content {
  height: 100%;
overflow-x: hidden;
  clear: both;
}

.admin-right span {
  /* border: 1px solid #ccc; */
}
.adminstration-left {
  float: left;
  width: 200px;
  height: 100%;
  border-right: 1px solid rgba(0, 0, 0, 0.2);
}
.admin-mes {
  float: right;
}
.admin-mes-tip,
.admin-main-name,
.cancel-admin {
  display: inline-block;
}
input {
  height: 35px;
  width: 200px;
  background: transparent;
  border: none;
  border: 1px solid #ccc;
}
.admin-right .admin-search{
  position: relative;
  float: left;
}
.admin-right .admin-search i{
  font-size:30px;
  color: black;
}
li {
  display: inline-block;
  text-align:left;
  line-height: 40px;
  padding: 10px 0px 0px 15px;
  -webkit-transition: all 0.2s linear;
  -moz-transition: all 0.2s linear;
  transition: all 0.2s linear;
  font-size: 18px;
  color: rgba(0, 0, 0, 0.9);
  text-shadow: 0 1px 0 rgba(0, 0, 0, 0.1);
  width: 115px;
  position: relative;
  z-index: 2;
  font-weight: 700;
}
li::after {
  content: "";
  display: inline-block;
  width: 3px;
  height: 39px;

  background: -webkit-linear-gradient(
    left,
    rgba(0, 0, 0, 0.2) 0%,
    rgba(0, 0, 0, 0.2) 100%
  );
  background: linear-gradient(
    to right,
    rgba(0, 0, 0, 0.2) 0%,
    rgba(0, 0, 0, 0.2) 100%
  );
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  -webkit-transition: all 0.2s linear;
  -moz-transition: all 0.2s linear;
  transition: all 0.2s linear;
}
.liactive{
  cursor: pointer;
  text-decoration: none;
  color: white;
  background: -webkit-linear-gradient(
    left,
    rgba(0, 0, 0, 0.2) 0%,
    rgba(0, 0, 0, 0) 100%
  );
  background: linear-gradient(
    to right,
    rgba(0, 0, 0, 0.2) 0%,
    rgba(0, 0, 0, 0) 100%
  );
  width: 100%;
}
li:hover {
  cursor: pointer;
  text-decoration: none;
  color: white;
  background: -webkit-linear-gradient(
    left,
    rgba(0, 0, 0, 0.2) 0%,
    rgba(0, 0, 0, 0) 100%
  );
  background: linear-gradient(
    to right,
    rgba(0, 0, 0, 0.2) 0%,
    rgba(0, 0, 0, 0) 100%
  );
  width: 100%;
}
a{
  display: inline-block;
  width:100%;
  height: 100%;
  transition:all 0.2s;
}
a:link{
   color:#666;
}
a:visited{
  color:#666;
}
a:active{
  color:white;
}
</style>