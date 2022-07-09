<template>
  <div id="app">

    <NavBar />

    <div id="contents">
      <h1 style="">Conference Deadlines</h1>
      <p>Countdowns to top __ __ __ conference deadlines.</p>

      <div id="incoming_conf" v-for="data in myData" :key="data.name">
        <ConfItem 
          v-if="(new Date(data.deadline).getTime() - new Date().getTime() >= 0)"
          :name="data.name"
          :deadline="data.deadline"
          :location="data.location"
          :url="data.url"
        />
      </div>

      <br>
      <br>

      <h1>Past Conferences</h1>
      <div class="ui divider"></div>

      <div id="past_conf" v-for="data in myData" :key="data.name + 'past'">
        <PastConf 
          v-if="(new Date(data.deadline).getTime() - new Date().getTime() < 0)"
          :name="data.name"
          :deadline="data.deadline"
          :location="data.location"
          :url="data.url"
        />
      </div>

    </div>
    
    
  </div>
</template>

<script>
import NavBar from './components/Navbar.vue'
import ConfItem from "./components/ConfItem.vue"
import PastConf from "./components/PastConf.vue"
import json from './data/data.json'

export default {
  name: 'App',
  components: {
    NavBar,
    ConfItem,
    PastConf
  },
  data(){
    return{
      myData: json.confs.sort(this.sort_by_date)
    }
  },
  methods: {
    sort_by_date: function(a, b){
      return new Date(a.deadline).getTime() - new Date(b.deadline).getTime();
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#contents {
  padding-top: 25px;
  padding-left: 25%;
  padding-right: 25%;
  text-align: left;
}

@media (max-width: 979px) {
  #contents {
    padding-top: 25px;
    padding-left: 5%;
    padding-right: 5%;
    text-align: left;
  }
}
</style>
