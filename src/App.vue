<template>
  <div id="app">
    <Header/>
    <div class="main">
      <router-view name="slidebar"></router-view>
      <router-view name="main"></router-view>
    </div>
  </div>     
</template>

<script>
import Header from './components/Header'
import Postlist from './components/Postlist'
export default {
  name: 'App',
  components:{
    Header,
    Postlist
  }
}
</script>

<style>
.main{
  width: 80%;
  margin: 0 auto;
}
@media (max-width: 678px){
  .main{
    width:100%;
  }
}
</style>
