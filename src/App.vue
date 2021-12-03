<template>
  <div id="app">

    <div class="container-job">
      <Jobcard v-for="item,index in getArrayJson" :key="index" :job="item"/>
    </div>
  </div>
</template>

<script>
import * as dataJson from "../exo-ressources/data.json"
import Jobcard from "./components/Jobcard.vue"
export default {
  name: 'App',
  components:{
    Jobcard
  },
  data(){
    return{
      dataTab: this.getArrayJson()
    }
  },

  computed:{
    getArrayJson(){
      var tab = []
      for(let key in dataJson){
        for(let key1 in dataJson[key] ){
          if(key1 =="logo"){
            dataJson[key][key1].logo = require(dataJson[key][key1])
          }
          tab.push(dataJson[key][key1])
        }
      }

      return tab;
      
    }
  }
}


</script>

<style scoped lang="scss">

#app{
  margin: 0;
  padding: 20px;
  width: 100vw;
  height: fit-content;
  min-height: 100vh;
  background-color: rgb(225, 248, 250);

}
</style>
