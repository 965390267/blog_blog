<template>
  <div id='wrap-music' ref='wrap' class="container" @mousedown="drag">
  
    <div id="BadApplePlayer" class="show ksclrc showAlbumList playing" style="background: rgba(99, 99, 99, 0.8); left: 0px;">
  
      <div class="player">
  
        <div class="blur-img"> <img class="blur" style="top: 0px; display: inline;" src="https://p3.music.126.net/Y1kh5LFIxjPut9_T81JIyw==/18635622580877743.jpg?param=300y300"> </div>
  
        <div class="infos">
  
          <div class="songstyle"> <i class="fa fa-music"></i> <span class="song"><span title="9妹 - 不气盛叫年轻人吗">9妹 - 不气盛...</span></span>
  
          </div>
  
          <div class="timestyle"> <span class="time">01:09 / 04:06</span> <i class="fa fa-clock-o"></i></div>
  
          <div class="artiststyle"> <i class="fa fa-user"></i> <span class="artist"><span title="9妹">9妹</span></span> <span class="moshi">顺序播放 <i class="fa fa-retweet"></i></span> </div>
  
          <div class="artiststyle"> <i class="fa fa-folder"></i> <span class="artist1"><span title="电音女皇">电音女皇</span></span> <span class="geci">Lrc歌词关闭 <i class="fa fa-check-circle"></i></span> </div>
  
        </div>
  
        <div class="control"> <i class="playtype fa current fa-retweet" title="切换模式"></i> <i class="prev fa fa-backward" title="上一首"></i>
  
          <div class="status" style="background-image: linear-gradient(90deg, rgb(108, 105, 113) 50%, transparent 50%, transparent), linear-gradient(191.598deg, rgb(0, 188, 212) 50%, rgb(108, 105, 113) 50%, rgb(108, 105, 113));">
  
          <b>					<i class="play fa fa-play" title="播放"></i>					<i class="pause fa fa-pause" title="暂停"></i>				</b> </div> <i class="next fa fa-forward" title="下一首"></i> <i class="search fa fa-search" title="搜索歌曲"></i> </div>
  
        <div class="bottom">
  
          <div class="playprogress">
  
            <div class="progressbg">
  
              <div class="progressbg1" style="width: 28%;"></div>
  
              <div class="progressbg2" style="left: 0%; width: 100%;"></div>
  
              <div class="ts" style="left: 28%;"></div>
  
            </div>
  
          </div>
  
          <ul class="bottomright">
  
            <li class="ratecontrol">
  
              <div class="rate fa fa-fast-forward" title="播放变速"></div>
  
              <div class="rateprogress">
  
                <div class="progressbg">
  
                  <div class="progressbg1" style="height: 100px;"></div>
  
                  <div class="ts" style="top: 0px;"></div>
  
                </div>
  
              </div>
  
            </li>
  
            <li class="volumecontrol">
  
              <div class="volume fa fa-volume-down" title="音量控制"></div>
  
              <div class="volumeprogress">
  
                <div class="progressbg">
  
                  <div class="progressbg1" style="height: 39px;"></div>
  
                  <div class="ts" style="top: 53px;"></div>
  
                </div>
  
              </div>
  
            </li>
  
            <li class="switch-ksclrc" style="display: list-item;"><i class="fa fa-toggle-off" title="打开歌词"></i></li>
  
            <li class="switch-playlist"><i class="fa fa-bars" title="播放列表"></i></li>
  
          </ul>
  
          <div style="clear:both"></div>
  
        </div>
  
        <div class="cover coverplay"><img src="https://p3.music.126.net/Y1kh5LFIxjPut9_T81JIyw==/18635622580877743.jpg?param=300y300"></div>
  
      </div>
  
      <div class="playlist">
  
        <div class="playlist-bd">
  
          <div class="album-list">
  
            <div class="musicheader">情殇博客(4)</div>
  
            <div class="list mCustomScrollbar _mCS_2 _mCS_3">
  
              <div class="mCustomScrollBox mCS-light" id="mCSB_3" style="position:relative; height:100%; overflow:hidden; max-width:100%;">
  
                <div class="mCSB_container mCS_no_scrollbar" style="position:relative; top:0;">
  
                  <ul>
  
                    <li class="current"><i class="fa fa-angle-right"></i><span class="index">1</span><span class="artist">当前播放&nbsp;&gt;&nbsp;</span>music&nbsp;-&nbsp;rong</li>
  
                    <li><i class="fa fa-angle-right"></i><span class="index">2</span><span class="artist"></span>MC另类&nbsp;-&nbsp;rong</li>
  
                    <li><i class="fa fa-angle-right"></i><span class="index">3</span><span class="artist"></span>Come on ！&nbsp;-&nbsp;rong</li>
  
                    <li><i class="fa fa-angle-right"></i><span class="index">4</span><span class="artist"></span>我搜索的歌曲&nbsp;-&nbsp;Me</li>
  
                  </ul>
  
                </div>
  
                <div class="mCSB_scrollTools" style="position: absolute; display: none;">
  
                  <div class="mCSB_draggerContainer">
  
                    <div class="mCSB_dragger" style="position: absolute; top: 0px;" oncontextmenu="return false;">
  
                      <div class="mCSB_dragger_bar" style="position:relative;"></div>
  
                    </div>
  
                    <div class="mCSB_draggerRail"></div>
  
                  </div>
  
                </div>
  
              </div>
  
            </div>
  
          </div>
  
          <div class="song-list">
  
            <div class="musicheader"> <i class="fa fa-angle-right"></i> <span>我搜索的歌曲(0)</span> </div>
  
            <div class="list mCustomScrollbar _mCS_1" data-album="3">
  
              <div class="mCustomScrollBox mCS-light" id="mCSB_1" style="position:relative; height:100%; overflow:hidden; max-width:100%;">
  
                <div class="mCSB_container mCS_no_scrollbar" style="position:relative; top:0;">
  
                  <ul></ul>
  
                </div>
  
                <div class="mCSB_scrollTools" style="position: absolute; display: none;">
  
                  <div class="mCSB_draggerContainer">
  
                    <div class="mCSB_dragger" style="position: absolute; top: 0px;" oncontextmenu="return false;">
  
                      <div class="mCSB_dragger_bar" style="position:relative;"></div>
  
                    </div>
  
                    <div class="mCSB_draggerRail"></div>
  
                  </div>
  
                </div>
  
              </div>
  
            </div>
  
          </div>
  
        </div>
  
      </div>
  
      <div class="switch-player" style="background: rgba(99, 99, 99, 0.298039);"> <i class="fa fa-angle-right" style="margin-top: 20px;"></i> </div>
  
      <div class="searchbox" style="background: rgba(99, 99, 99, 0.298039); display: none;"><input type="text" placeholder="输入歌手+歌曲名并回车..."><i title="清空搜索播放列表" class="delsearchlist fa fa-trash"></i>
  
        <div class="searchlistbox">
  
          <ul style="background: rgba(99, 99, 99, 0.8);"></ul>
  
        </div>
  
      </div>
  
    </div>
  
    <audio @canplaythrough="loadmusic" :src='musicsrc' ref='controlmusic' controls></audio>
  
    <!-- <div class="box">        
  
              <div class="page"></div>
  
              <div class="page"></div>
  
              <div class="page"></div>
  
              <div class="page"></div>
  
              <div class="page"></div>
  
              <div class="page"></div>
  
          </div> -->
  
  </div>
</template>

<script>
  export default {
  
    data() {
  
      return {
  
        hascolor: -1,
  
        musics: [],
  
        x: 0,
  
        y: 0,
  
        distx: 0,
  
        disty: 0,
  
        musicsrc: ""
  
      };
  
    },
  
    methods: {
  
      drag(e) {
  
        var Left = e.target;
  
        var leftw = Left.offsetWidth / 2;
  
        var lefth = Left.offsetHeight / 2;
  
        document.onmousemove = function(e) {
  
          e.preventDefault();
  
          this.distx = e.clientX - leftw;
  
          this.disty = e.clientY - 10;
  
          // -startX;
  
          Left.style.top = this.disty + "px";
  
          Left.style.left = this.distx + "px";
  
        };
  
  
  
        document.onmouseup = function() {
  
          localStorage.setItem("x", 0);
  
  
  
          localStorage.setItem("y", this.disty);
  
          document.onmousemove = null;
  
        };
  
      },
  
      loadmusic() {
  
        this.$refs.controlmusic.play();
  
      },
  
      choosemusic(m, index) {
  
        this.hascolor = index;
  
        // var xhr = new XMLHttpRequest();
  
        // var decodebuff = null;
  
        // var ac = new AudioContext();
  
        // function load(url) {
  
        //   xhr.open("GET", url);
  
        //   xhr.responseType = "arraybuffer";
  
        //   xhr.onreadystatechange = function() {
  
        //     ac.decodeAudioData(xhr.response, function(buffer) {
  
        //       decodebuff = buffer;
  
        //       var source = ac.createBufferSource();
  
        //       source.buffer = decodebuff;
  
        //       source.connect(ac.destination);
  
  
  
        //       var gainnnode = ac.createGain();
  
        //       source.connect(gainnnode);
  
        //       gainnnode.connect(ac.destination);
  
        //       gainnnode.gain.value = 0.1;
  
        //       source.start(0);
  
        //     });
  
        //   };
  
        //   xhr.send();
  
        // }
  
        this.musicsrc = "http://localhost:3000/media/" + m;
  
        //  setTimeout(()=>{
  
  
  
        //  })
  
  
  
        // load("http://localhost:3000/media/" + m);
  
      }
  
    },
  
    mounted() {
  
      var node = this.$refs.wrap;
  
      node.style.top = Number(localStorage.getItem("y")) + "px";
  
      node.style.left = Number(localStorage.getItem("x")) + "px"; //读取本地存储的位置信息给div设置位置
  
      // this.dragbox();
  
      this.$http.get("/api/music").then(response => {
  
        this.musics = response.data.musicnames;
  
      });
  
    }
  
  };
</script>

<style scoped>
 
  #BadApplePlayer .player {
    cursor: move;
    position: relative;
    overflow: hidden;
    text-shadow: none;
    background-color: rgba(0,0,0,0.1);
    height: 180px;
    border-radius: 5px 5px 0 0;
}

#XlchPlayer * {
    box-sizing: content-box;
    list-style-type: none;
}
  #XlchPlayer .blur-img {
    width: 365px;
    height: 155px;
    position: absolute;
}
#XlchPlayer .blur {
    display: none;
    position: relative;
    width: 365px;
    height: 155px;
    /* filter: url(blur.svg#blur); */
    -webkit-filter: blur(20px);
    -moz-filter: blur(20px);
    -ms-filter: blur(20px);
    filter: blur(20px);
    filter: progid:DXImageTransform.Microsoft.Blur(PixelRadius=20, MakeShadow=false);
}

#BadApplePlayer .player .infos {
    position: absolute;
    top: 15px;
    left: 10px;
    color: #fff;
    text-shadow: 1px 1px 1px #000;
    font-weight: bolder;
}
#XlchPlayer .fa {
    width: initial;
}
#XlchPlayer * {
    box-sizing: content-box;
    list-style-type: none;
}
.fa {
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
.fa {
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
.fa {
    display: inline-block;
    font-family: FontAwesome;
    font-style: normal;
    font-weight: normal;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
i {
    display: inline-block;
    font: normal normal normal 14px/1 'Elusive-Icons';
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    transform: translate(0, 0);
}
i {
    color: #555;
}
i {
    color: #ff6700;
    margin-right: 5px;
}
#BadApplePlayer .player .infos {
    position: absolute;
    top: 15px;
    left: 10px;
    color: #fff;
    text-shadow: 1px 1px 1px #000;
    font-weight: bolder;
}
#XlchPlayer * {
    box-sizing: content-box;
    list-style-type: none;
}
Inherited from div.player
#BadApplePlayer .player {
    cursor: move;
    position: relative;
    overflow: hidden;
    text-shadow: none;
    background-color: rgba(0,0,0,0.1);
    height: 180px;
    border-radius: 5px 5px 0 0;
}
#BadApplePlayer .player .infos {
    position: absolute;
    top: 15px;
    left: 10px;
    color: #fff;
    text-shadow: 1px 1px 1px #000;
    font-weight: bolder;
}
#XlchPlayer * {
    box-sizing: content-box;
    list-style-type: none;
}
Inherited from div.player
#BadApplePlayer .player {
    cursor: move;
    position: relative;
    overflow: hidden;
    text-shadow: none;
    background-color: rgba(0,0,0,0.1);
    height: 180px;
    border-radius: 5px 5px 0 0;
}
#BadApplePlayer {
    font-size: 13px;
    -webkit-transition: height .5s;
    -moz-transition: height .5s;
    -ms-transition: height .5s;
    transition: height .5s;
    text-align: left;
    color: #38343e;
    width: 365px;
    position: fixed;
    bottom: 40px;
    box-shadow: 0 0 5px 5px rgba(0,0,0,0.2);
    border-radius: 5px;
    z-index: 5000;
    height: 181px;
}
  
</style>
