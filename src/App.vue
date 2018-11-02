<template>
  <div id="app">
      <div class="left">
        <leftNav></leftNav>
      </div>
      <div>
        <router-view ></router-view>
      </div>
  </div>
</template>

<script>
  import leftNav from '@/components/leftNav'
export default {
  name: 'App',
  components:{
    leftNav
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    height: 100%;
  }
  .left{
    height: 100%;
    float: left;
  }
  .left-nav{
        width: 100px;
        height: 100%;
        background: #252525;
  }
  .left-nav li{
    list-style: none;
    color:#d92353;
    text-align:center;
    height: 100px;
    padding-top:20px; 
  }
  .iconfont{
    font-size: 24px;
  }
</style>
