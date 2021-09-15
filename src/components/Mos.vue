//https://api.hatchways.io/assessment/students
<template>
    <div class="flex-container">
        <div class="item"><img width="100" :src="pic" /></div>
        <div class="itemm">
            <p class="bdy">
                <span class="h3">{{fn}} {{ln}}</span><br>
                city: {{city}}<br>
                email: {{email}}<br>
                company: {{company}}<br>
                skill: {{skill}}<br>
                average: {{average(grades)}}% <br>
                

            </p>
                <div class="bdy" :class="{ 'd-none': !isActive}">
                    <table v-for="(g, i) in grades" :key="i">
                        <Grade :testName="i" :grade="g" />
                    </table>
                </div>

            <Tag :tags="tags" />
            <input type="text" class="d-block w-100 inputLargeTag"  placeholder="Add Tag" v-model="addTags" v-on:keyup.enter="addTag">
        </div>
        <div class="item"><button @click="showGrades()" class="fas fa-plus largeFont" style="color:rgb(99, 99, 99);"></button></div>
    </div>
</template>

<script>
import Grade from './Grade'
import Tag from './Tag'
export default{
    name:'Mos',
    components:{
        Grade,
        Tag
    },
    mounted() {
    // Use the parent function directly here
  },
    props:{
        image:{type: String},
        title:{type: String},
        city:{type: String},
        company:{type: String},
        email:{type: String},
        fn:{type: String},
        avr: {type:Number},
        grades:{type: Array},
        id:{type: Number},
        ln:{type: String},
        pic:{type: String},
        skill:{type: String},
        tag:{type:Array},
    },
    methods:{
        showGrades: function(){
            this.isActive = !this.isActive;
            
        },
        average: function(data){
            let total = 0;
        
            for(let i = 0; i< data.length; i ++){
                total = total+ parseInt(data[i])/100;
            }
            //console.log(data);
            return Math.round((total/data.length)*100)
            
        },
        addTag(){
            
          this.tags.push(this.addTags)
          this.$emit('updateTags',this)
         // console.log(this.addTags)
          
      
  }, 
  showTags(){
      alert("hello world")
      this.$emit('showTags', this)
  }
    },
    computed: {
  classObject() {
    return {
      active: this.isActive,
    }
  },
  
    },

    data(){
        return{
        isActive:false,
        tags:[],
        addTags:''
       //return {avr : this.average(this.grades)}
       }
    }
}
</script>

<style scope>
.inputLargeTag{
  font-size: .5em;

  outline: 0;
  border-width: 0 0 2px;
  border-color: rgb(61, 61, 61, .133);
  padding-top:20px;
  padding-bottom:20px;
}
.img{
    position:relative;
    display:block;
    float:left;
}

.largeFont{
    font-size: larger;
}
button{
    background-color:white;
    border: 0;
}
.d-none{
    display:none;
}
.d-block{
    display:block;
}
img{
    background-color:#fff;
    border:1px solid red;    
    height:100px;
    border-radius:50%;
    -moz-border-radius:50%;
    -webkit-border-radius:50%;
    width:100px;
}
.item{
    flex-grow: 1;
}
.itemm{
    flex-grow: 2;
}
.bdy{
    font-size:.7em;
    text-align:left;
    margin-top: 0px;
}

.h3{
    text-align:left;
    font-size:1.1em;
    font-weight: bold;
    margin-bottom:10px;
    margin-top:0px;
}
.tal{
    text-align: left;
}
p{
    font-size: 1em;
}
.w-40{
    width:30%;
}
.w-60{
    width:70%;
}
.container {
  flex-direction: row ;
  flex-wrap: nowrap;
}

.flex-container {
  display: flex;
  width:100%;
  margin-left:auto;
  margin-right:auto;
  
}

.flex-container > div {
  
  margin: 10px;
  padding: 20px;
  font-size: 30px;
}

</style>
