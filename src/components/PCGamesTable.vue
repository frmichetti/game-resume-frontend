<template>
  <br />
  <br />
  <br />
  <div class="input-group mb-3">
    <div class="input-group-prepend">
      <span class="input-group-text" id="basic-addon1">Search</span>
    </div>
    <input type="text" class="form-control" placeholder="Input Game Name" aria-label="Search" aria-describedby="basic-addon1" v-model="searchQuery">
  </div>



    <table class="table table-striped table-hover">
    <thead>
      <tr>
        <th>AppId</th>
        <th>System</th>
        <th>Title</th>        
        <th>Finished ?</th>
      </tr>
    </thead>
    <tbody>  
      <tr v-for="game, idx in resultQuery" :key="idx">
        <td>{{game.app_id }}</td>
        <td>{{game.system}}</td>
        <td>{{game.title}}</td>            
        <td><input type="checkbox" v-model="game.finished" :disabled=true></td>        
      </tr>
    </tbody>   
</table>
</template>

<script>

import axios from 'axios';

export default {
  name: 'PCGamesTable',
  data() {
    return {
      searchQuery: null,
      games: []      
    }
  },
  created() {
    axios.get(`${process.env.VUE_APP_BACKEND_SERVER}/pc`).then((resp) =>{
      this.games = resp.data.games;      
    });    
  },
  computed: {
    resultQuery() {
    if(this.searchQuery){
      return this.games.filter((item)=>{        
        return this.searchQuery.toLowerCase().split(' ').every(v => item.title.toLowerCase().includes(v))
      })
      }else{
        return this.games;
      }
  }  
}    
}
</script>

<style scoped>

</style>