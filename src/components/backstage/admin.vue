<template>
<div id='admin'>
   <div v-if='mainshow' class="page-container">
            <h1>Login</h1>
            <form action="" method="post">
                <input type="text" name="username" @keydown.enter="enter" v-model="usename" class="username" placeholder="Username">
                <input type="password" name="password" @keydown.enter="enter" v-model="password" class="password" placeholder="Password">
                <div class="submit-person"  @click='enter' >Sign me in</div>
                <div class="error"><span>+</span></div>
            </form>
            <div class="connect">
                
                <p>
                    <a class="facebook" href="">㉢ZZH博客后台管理系统</a>
                    <a class="twitter" href=""></a>
                </p>
            </div>
        </div>
     <canvas id='canv'></canvas>  
     <div v-if="showalert" class="alert-success">
       <h3 class="alert-content">登陆成功</h3>
     </div>
</div>

</template>
<script>
import {hex_md5} from '../../assets/js/md5.js'
export default {
  data() {
    return {
      mainshow:true,
      showalert:false,
      usename: "",
      password: ""
    };
  },
  methods: {
    ball() {
      document.addEventListener("resize", resize);

      function resize() {
        canvs.width = window.innerWidth;

        canvs.height = window.innerHeight;
      }
      var canvs = document.getElementById("canv");

      canvs.width = window.innerWidth;

      canvs.height = window.innerHeight;

      var ctx = canvs.getContext("2d");

      var ball = function() {
        this.bx = Math.random() * canvs.width;

        this.by = Math.random() * canvs.height;

        this.r = Math.random() * 20 + 10;

        this.color =
          "rgba(" +
          Math.ceil(Math.random() * 255) +
          "," +
          Math.ceil(Math.random() * 255) +
          "," +
          Math.ceil(Math.random() * 255) +
          "," +
          Math.random() / 4 +
          ")";

        this.vx = Math.random() * 3 - 2;

        this.vy = Math.random() * 3 - 2;
      };
      ball.prototype.draw = function() {
        // ctx.fillStyle = 'rgba(255,255,255,0.1)';
        //  ctx.fillRect(0, 0, canvs.width, canvs.height);
        // ctx.clearRect(0, 0, canvs.width, canvs.height);
        ctx.beginPath();
        var grd = ctx.createRadialGradient(
          this.bx,
          this.by,
          0,
          this.bx,
          this.by,
          this.r
        );
        grd.addColorStop(0, "white");
        grd.addColorStop(1, this.color);
        ctx.globeAlpha = 0.2;
        // Fill with gradient
        ctx.fillStyle = grd;

        ctx.arc(this.bx, this.by, this.r, 0, Math.PI * 2, true);

        ctx.fill();
      };

      ball.prototype.move = function() {
        this.bx += this.vx;

        this.by += this.vy;

        // ball.vy *= 0.99;
        // ball.vy += 0.25;
        if (this.by + this.vy > canvs.height || this.by + this.vy < 0) {
          this.vy = -this.vy;
          //
        }
        if (this.bx + this.vx > canvs.width || this.bx + this.vx < 0) {
          this.vx = -this.vx;
          // nball.color = '#' + ('00000' + ((Math.random() * 16777215)))
        }
      };

      function gogo(num) {
        num = num || 10;
        var globe = [];

        for (var i = 0; i < num; i++) {
          var nball = new ball();

          globe.push(nball);

          // nball.draw()
        }

        function ballmove() {
          //     ctx.fillStyle = 'rgba(255,255,255,0.3)';
          //  ctx.fillRect(0, 0, canvs.width, canvs.height);
          ctx.clearRect(0, 0, canvs.width, canvs.height);
          for (var j = globe.length - 1; j >= 0; j--) {
            // globe[j].draw()

            globe[j].move();

            globe[j].draw();
          }
          window.requestAnimationFrame(ballmove);
        }
        ballmove();
      }
      gogo(canvs.width / 50);

      // function drawcrc() {
      //     // ctx.fillStyle = 'rgba(255,255,255,0.3)';
      //     // ctx.fillRect(0, 0, canvs.width, canvs.height);
      //     ctx.clearRect(0, 0, canvs.width, canvs.height);
      //     var nball = new ball();
      //     nball.draw();

      //     window.requestAnimationFrame(drawcrc)
      // }
      // drawcrc();
    },
    enter() {
      if (this.usename === "" && this.password === "") {
        alert("用户名和密码不能为空");
      } else {
        if (this.usename === "") {
          alert("请输入您的用户名");
        }
        if (this.password === "") {
          alert("请输入您的密码");
        }
      }
      if (this.usename !== "" && this.password !== "") {
        // console.log( hex_md5(this.usename), hex_md5(this.password));
    //        sessionStorage.setItem('usename',hex_md5(this.usename));
    // sessionStorage.setItem('password',hex_md5(this.password))
    let md5name=hex_md5(this.usename),md5password=hex_md5(this.password);
        this.$http
          .post("api/login", {
            params: {
              usename:md5name,
              password: md5password
            }
          })
          .then(response => {
            // console.log(response.data);
            if(response.data.pass=='ok'){
              // alert('登陆成功')
              this.showalert=true;
              this.mainshow=false;
              sessionStorage.setItem('usename',md5name);
              sessionStorage.setItem('password',md5password);
              setTimeout(()=>{
  this.$router.push({path:'/adminstration/allmes'})
              },500)
              
            }else{
                alert('您输入的账号或密码错误')
            }
          });


      }
    }
  },
  mounted() {
    this.ball();
    this.showalert=false;
    this.mainshow=true;

  }
};
</script>

<style scoped>
#admin {
  
  background-image: url("../../assets/images/starsky.jpg");
  background-size: 100% 100%;
}
canvas {
  position: absolute;
  top: 0px;
  left: 0px;
}
.page-container {
  z-index: 99;
  margin: 200px auto 0 auto;
}
h1 {
  font-family: "Roboto Slab", serif;
  margin: 0 auto;
  text-align: center;
  color: rgb(231, 158, 203);
  font-size: 30px;
  font-weight: 700;
  text-shadow: 0 1px 4px rgba(0, 0, 0, 0.2);
}
form {
  position: relative;
  z-index: 10;
  width: 305px;
  margin: 15px auto 0 auto;
  text-align: center;
}
input {
  width: 270px;
  height: 42px;
  margin-top: 25px;
  padding: 0 15px;
  background: #2d2d2d;
  background: rgba(45, 45, 45, 0.15);
  -moz-border-radius: 6px;
  -webkit-border-radius: 6px;
  border-radius: 6px;
  border: 1px solid #3d3d3d;
  border: 1px solid rgba(255, 255, 255, 0.15);
  -moz-box-shadow: 0 2px 3px 0 rgba(0, 0, 0, 0.1) inset;
  -webkit-box-shadow: 0 2px 3px 0 rgba(0, 0, 0, 0.1) inset;
  box-shadow: 0 2px 3px 0 rgba(0, 0, 0, 0.1) inset;
  /* font-family: "PT Sans", Helvetica, Arial, sans-serif; */
  font-size: 18px;
  
  color: rgb(95, 207, 211);
  text-shadow: 0 1px 2px rgba(231, 98, 98, 0.1);
  -o-transition: all 0.2s;
  -moz-transition: all 0.2s;
  -webkit-transition: all 0.2s;
  -ms-transition: all 0.2s;
}
.submit-person {
  cursor: pointer;
  width: 300px;
  height: 44px;
  line-height: 44px;
  margin-top: 25px;
  padding: 0;
  background: #ef4300;
  -moz-border-radius: 6px;
  -webkit-border-radius: 6px;
  border-radius: 6px;
  border: 1px solid #ff730e;
  -moz-box-shadow: 0 15px 30px 0 rgba(255, 255, 255, 0.25) inset,
    0 2px 7px 0 rgba(0, 0, 0, 0.2);
  -webkit-box-shadow: 0 15px 30px 0 rgba(255, 255, 255, 0.25) inset,
    0 2px 7px 0 rgba(0, 0, 0, 0.2);
  box-shadow: 0 15px 30px 0 rgba(255, 255, 255, 0.25) inset,
    0 2px 7px 0 rgba(0, 0, 0, 0.2);
  font-family: "PT Sans", Helvetica, Arial, sans-serif;
  font-size: 14px;
  font-weight: 700;
  color: #fff;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  -o-transition: all 0.2s;
  -moz-transition: all 0.2s;
  -webkit-transition: all 0.2s;
  -ms-transition: all 0.2s;
}
.error {
  display: none;
  position: absolute;
  top: 27px;
  right: -55px;
  width: 40px;
  height: 40px;
  background: #2d2d2d;
  background: rgba(45, 45, 45, 0.25);
  -moz-border-radius: 8px;
  -webkit-border-radius: 8px;
  border-radius: 8px;
}
.error span {
  display: inline-block;
  margin-left: 2px;
  font-size: 40px;
  font-weight: 700;
  line-height: 40px;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  -o-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
}
.connect {
  position: absolute;
  bottom: 10px;
  left: 50%;

  transform: translateX(-50%);
}
.connect a {
  color: rgb(160, 201, 236);
}
.alert-success{
  /* margin: -200px auto; */
   
    position: absolute;
       top: 33%;
    left: 39%;
  background: #2e3846;
width: 300px;
text-align: center;
padding: 30px 0;
color: aliceblue;
    height: auto;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    border-radius: 3px;
    -webkit-background-clip: padding-box;
    -moz-background-clip: padding-box;
    background-clip: padding-box;
    -webkit-box-shadow: 0 2px 4px 0 rgba(0,0,0,0.3);
    -moz-box-shadow: 0 2px 4px 0 rgba(0,0,0,0.3);
    box-shadow: 0 2px 4px 0 rgba(0,0,0,0.3);
}
</style>
