<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Github Users</h3>
    <div>
      <input type="text" placeholder="enter the name you search" v-model="userName"/>
      <button @click="search">Search</button>
    </div>
  </section>
</template>

<script>
import PubSub from 'pubsub-js'
export default {
  data(){
    return{
      userName:''
    }
  },
  methods:{
    search(){
      let userName=this.userName.trim();
      if(userName){
        PubSub.publish('search',userName)
      }
    }
  }
}
</script>

<style>

</style>
