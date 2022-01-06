<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <br>
    <input v-model="path" style="text-align:center;">
    <p class="bg-gray" 
      v-clipboard:copy="transformPath" 
      v-clipboard:success="onCopy" 
      v-clipboard:error="onError">
      {{transformPath}}
    </p>
    <p v-show="status" class="status success">複製成功</p>
    <p v-show="status===false" class="status fail">複製失敗</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      path:"",
      status:null
    }
  },
  computed:{
    transformPath(){
      return this.path.replace(/\\/g,'/')
    }
  },
  watch:{
    path(){
      if(!this.path){
        this.status = null
      }
    }
  },
  methods:{
    onCopy(){
      this.status = true
      setTimeout(()=>{this.status=null},2000,this)
    },
    onError(){
      this.status = truefalsea
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 40px;
}
input{
  font-size: 40px;
  width: 1000px;
}
.bg-gray{
  background-color: gray;
  color: white;
}
.status{
  font-size: 16px;
  animation-duration: 2s;
  animation-name: fade;
}
@keyframes fade {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }
.success{
  color: green;
}
.fail{
  color: red;
}
</style>
