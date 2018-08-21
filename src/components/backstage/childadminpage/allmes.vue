<template>
  <div class="total-mes">
      <h1 class="mes-tit">信息总览</h1>
      <div class="mes-show">
          <ul class="mes-show-ul">
              <li class="article-num"><h4>文章</h4><span>0条</span></li>
               <li class="article-num"><h4>评论</h4><span>0条</span></li>
                <li class="article-num"><h4>访问量</h4><span>0条</span></li>
                 <li class="article-num"><h4>文章</h4><span>0条</span></li>
                
          </ul>
      </div>
      <h1 class="allmes-state">状态</h1>
      <div class="allmes-state-detail">登陆者:admin，第100次登陆</div>
      <div class="allmes-state-detail2">上次登录时间:2018-1-23,</div>
      <h1 class="allmes-system-tit">系统信息</h1>
      <div class="table-responsive">
        <table class="table table-striped table-hover">
          <thead>
            <tr> </tr>
          </thead>
          <tbody>
            <tr>
              <td>管理员个数:</td>
              <td>2 人</td>
              <td>服务器软件:</td>
              <td>Apache/2.4.10 (Win32) OpenSSL/1.0.1i mod_fcgid/2.3.9</td>
            </tr>
            <tr>
              <td>浏览器:</td>
              <td>Chrome47</td>
              <td>PHP版本:</td>
              <td>5.6.1</td>
            </tr>
            <tr>
              <td>操作系统:</td>
              <td>Windows 10</td>
              <td>PHP运行方式:</td>
              <td>CGI-FCGI</td>
            </tr>
            <tr>
              <td>登录者IP:</td>
              <td>::1:55570</td>
              <td>MYSQL版本:</td>
              <td>5.5.40</td>
            </tr>
            <tr>
              <td>程序版本:</td>
              <td class="version">YlsatCMS 1.0 <font size="-6" color="#BBB">(20160108160215)</font></td>
              <td>上传文件:</td>
              <td>可以 <font size="-6" color="#BBB">(最大文件：2M ，表单：8M )</font></td>
            </tr>
            <tr>
              <td>程序编码:</td>
              <td>UTF-8</td>
              <td>当前时间:</td>
              <td>2016-01-08 15:50:30</td>
            </tr>
          </tbody>
          <tfoot>
            <tr></tr>
          </tfoot>
        </table>
      </div>
  </div>
</template>
<script>
export default {
    data(){
        return{

        }
    },
    methods:{

    },
    mounted(){

    }
};
</script>

<style scoped>
.total-mes {
    font-family: '微软雅黑';
  width: 100%;
  margin-left: 210px;

}
.mes-show-ul li{
      font-family: '微软雅黑';
    width:23%;
display: inline-block;
text-align: center;
}
.mes-tit{
    padding: 15px;
    border-bottom: 1px solid #ccc;
}
.mes-show{
    margin-top: 15px;
}
/* .mes-show-ul::after{
    content: "";
        box-sizing: border-box;
    display: table;
clear: both;
} */
.allmes-state{
    border-bottom: 1px solid rgb(207, 92, 92);
    margin-bottom: 10px;
}
.allmes-state-detail{
    padding: 10px 0;
    background-color: rgba(0,0,0,.2);
}
.allmes-system-tit{
        border-bottom: 1px solid rgb(207, 92, 92);
}
.allmes-system-mes{
    margin-top: 10px;
}
.allmes-system-mes .first,.second{
        width:50%;
float: left;
text-align: center;
}
.first-one,.first-two li{
  
background-color: rgba(0,0,0,.2);
}

</style>
