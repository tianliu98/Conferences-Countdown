<template>
  <div id="app">

    <NavBar />

    <div id="contents">
      <h1 style="">Conference Deadlines</h1>
      <p>Contact the manager to add upcoming deadlines. Please use the following format.</p>
      <br>
      <p>{"name":"CONF-AA", "url":"https://www.google.com", "deadline": "Jul 22, 2022 15:37:25 GMT-5", "location": "XXXX, XX, XX"}</p>

      <div id="incoming_conf" v-for="data in myData" :key="data.name">
        <ConfItem 
          v-if="(new Date(data.deadline).getTime() - new Date().getTime() >= 0)"
          :name="data.name"
          :deadline="data.deadline"
          :location="data.location"
          :url="data.url"
          :is_expired=false
        />
      </div>

      <br>
      <br>

      <h1>Past Conferences</h1>
      <div class="ui divider"></div>

      <div id="past_conf" v-for="data in myData" :key="data.name + 'past'">
        <ConfItem 
          v-if="(new Date(data.deadline).getTime() - new Date().getTime() < 0)"
          :name="data.name"
          :deadline="data.deadline"
          :location="data.location"
          :url="data.url"
          :is_expired=true
        />
      </div>

    </div>
    
    
  </div>
</template>

<script>
import NavBar from './components/Navbar.vue'
import ConfItem from "./components/ConfItem.vue"
import json from './data/data.json'

export default {
  name: 'App',
  components: {
    NavBar,
    ConfItem,
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
