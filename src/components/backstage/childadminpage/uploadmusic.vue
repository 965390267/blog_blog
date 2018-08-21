<template>
  <div>
      
      <input type='file' @change="put($event)" multiple="multiple">
  
  <div class="kugoumusic">
      <div><input type='search'></div>
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
put(e){
console.log(e.target.files[0])
var formdata=new FormData();
formdata.append('upmusic',e.target.files[0])
 let config={ headers:{'Content-Type':'multipart/form-data'}}
 this.$http.post('api/uploadmusic',formdata,config).then(res=>{
    //  console.log(res)
 })
}
    },
    mounted(){


    }
};
</script>