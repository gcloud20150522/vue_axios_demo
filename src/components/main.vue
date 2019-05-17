<template>
  <div>
    <h1 v-if="firstView">输入名字进行搜索</h1>
    <h2 v-if="loading">loading...</h2>
    <p v-if="errorMsg">{{errorMsg}}</p>
    <div class="row">
      <div class="card" v-for="(user,index) in users" :key="index">
        <a :href="user.html_url" target="_blank">
          <img :src="user.avatar_url" style='width: 100px'/>
        </a>
        <p class="card-text">{{user.login}}</p>
      </div>
    </div>
  </div>

</template>

<script>
import PubSub from 'pubsub-js'
import Axios from 'axios'

export default {
  data(){
    return{
      firstView:true,
      loading:false,
      errorMsg:"",
      users:null
    }
  },
  mounted(){
    PubSub.subscribe('search',(msg,userName)=>{
      const url=`https://api.github.com/search/users?q=${userName}`;
      this.firstView=false;
      this.loading=true;
      this.users=null;
      Axios.get(url)
      .then(res=>{
        this.firstView=false;
        this.loading=false;
        this.users=res.data.items;
        console.log(res);
        
      })
      .catch(err=>{
        this.errorMsg=err
        
      })
    })
  }
}
</script>

<style>
.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}
</style>
