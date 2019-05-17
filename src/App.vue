<template>
<div id="app">
  <div class="container">
    <HeaderTop/>
    <MainC/>
  </div>
</div>
</template>

<script>
import HeaderTop from "./components/headerTop"
import MainC from "./components/main"

export default {
  name: 'App',
  components:{
    HeaderTop,MainC
  }
}
</script>

<style>

</style>
