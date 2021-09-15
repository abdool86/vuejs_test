<template>
    <tr>
        <td style="padding-right: 20px">Test {{testName}}</td><td>{{grade}}%</td>
    </tr>
</template>

<script>
    export default{
        name:'Grade',
        props:{
            testName:{type:Number},
            grade:{type:String}
        }
    }
</script>
