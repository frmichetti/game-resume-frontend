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
        <th>Idx</th>
        <th>Title</th>
        <th>System</th>
        <th>Finished ?</th>
      </tr>
    </thead>
    <tbody>  
      <tr v-for="game, idx in resultQuery" :key="idx">
        <td>{{idx + 1 }}</td>
        <td>{{game.title}}</td>    
        <td>{{game.system}}</td>
        <td><input type="checkbox" v-model="game.finished" :disabled=true></td>                
      </tr>
    </tbody>   
</table>
</template>

<script>
export default {
  name: 'FinishedGamesTable',
  props: {
    games: Array
  },
  data() {
    return {
      searchQuery: null    
    }
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