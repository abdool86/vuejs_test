<template>
 
    <div class="bg-white" style="padding:10px; border-radius: 15px;"> 
      <input type="text" class="d-block w-100 inputLarge" placeholder="Search by name" v-model="searchQuery">
      <input type="text" class="d-block w-100 inputLarge" placeholder="Search by Tags" v-model="searchTags">

      <Mos  v-for="d of resultQuery" 
      :key=d.id 
      :id=d.id :pic="d.pic" :fn="d.firstName" 
      :ln="d.lastName" :email="d.email" :company="d.company" 
      :city="d.city" :skill="d.skill" :grades="d.grades" 
       @showTags="showTags" 
      @updateTags="updateTags"/>
    <!--
    <div v-for="d in data" :key="d.id">
    <Mos  :pic="d.pic" :fn="d.firstName" :ln="d.lastName" :email="d.email" :company="d.company" :city="d.city" :skill="d.skill" :grades="d.grades" />
  </div>
  -->
    </div>
</template>

<script>
import Mos from './components/Mos.vue'
export default {
  name: 'App',
  mounted(){
    this.getData();
  
  },
  components: {
    Mos,
  }, 
  data(){
    return {
      datas:[],
      searchQuery: null,
      searchTags: null,
      tagsList:[],
    }
  },
  methods:{
    test(){
      return this.tags;
    },
    
    getData(){
      
      fetch("https://api.hatchways.io/assessment/students",{
        method: 'get'
      })
        .then(r => r.json())
        .then(json => {
          this.datas= this.fixJson(json.students);
        });
        console.log(this.datas)
        //this.addTags()
  
      console.log(this.datas)
    },
    

    fixJson(datas){
      for(var i = 0; i< datas.length; i++){
        datas[i].id =parseInt(datas[i].id)
        datas[i].tags = []
        for(var j = 0; j< this.tagsList; j++){
          if (this.tagsList[j] == datas[i].id){
            datas[i].tags = this.tagsList[j].tags;
          }
        }
        //datas[i].tags=[];

      }
      return datas;
    },
    showTags(e){
        for(var i = 0; i < this.tags; i ++){
          if (this.tags[i].id === e.id){
            alert("hello")
          }
        }
    },
    updateTags(e){
      if(!this.tagsList.some(tl=>tl.id===e.id)){

      this.tagsList.push({id:e.id,tags:e.tags})
      }
      console.log(this.tagsList)
    }
  },
 
  computed: {
        resultQuery() {
      if (this.searchQuery) {
        /*
        let sq = this.datas.filter(item => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every(v => item.firstName.toLowerCase().includes(v))
            .every(v => item.lastName.toLowerCase().includes(v));
        } );
        */
       let sq = this.datas.filter(item => 
         this.searchQuery
            .toLowerCase()
            .split(" ")
            .every(v => item.firstName.toLowerCase().includes(v))
         || 
         this.searchQuery
            .toLowerCase()
            .split(" ")
            .every(v => item.lastName.toLowerCase().includes(v))
        
        
        );
       
       return sq
      } else if(this.searchTags){
        return this.datas.filter(item => {
          return this.searchTags
            .toLowerCase()
            .split(" ")
            .every(v => item.tags.includes(v));
        });

      } else {

        return this.datas;
      }
      
    },
     

  }

}
</script>

<style>
body{
  background-color: rgba(231, 231, 231, 0.6);
}
.bg-white{
  background-color:white;
  width:60%;
  margin-left:auto;
  margin-right:auto;
}
.d-block{
  display: block;
}
.w-100{
  width:100%
}
.inputLarge{
  font-size: 1.5em;

  outline: 0;
  border-width: 0 0 2px;
  border-color: rgb(61, 61, 61, .133);
  padding-top:20px;
  padding-bottom:20px;
}
.inputLarge:focus{
  outline: 0;
  border-width: 0 0 2px;
  border-color: rgba(63, 63, 63, 0.315);
  
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  
}


</style>
