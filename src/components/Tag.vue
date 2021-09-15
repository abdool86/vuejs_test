<template>
    <span v-for="(t, i) of tags" :key="i" class="tag">{{t}}</span> 
</template>

<script>

export default{
    name:'Tag',

components:{
    
},props:{
    tags:{type:Array}
}
}
</script>


<style scope>
span.tag{
    float:left;
    background-color: rgb(102, 102, 102);
    color: white;
    padding:10px;
    margin-right: 5px;
    font-size: .8em;
    display:inline-block;
    border-radius: 5px;
}
</style>