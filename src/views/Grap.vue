<template>
<div><chartjs-bar v-bind:labels="labels" v-bind:datasets="datasets" v-bind:option="option"></chartjs-bar></div>
 
</template>

<script>    
import axios from 'axios'
export default {
    data(){
        return{
            
            labels: [ ],
            datasets:[{
                data:[],
                backgroundColor:["Red","Yellow","Purple","Red","Yellow","Purple","Red","Yellow","Purple","Purple","Purple","Purple","Purple","Yellow","Purple","Yellow","Purple","Yellow","Purple","Red","Yellow","Purple","Red","Yellow","Purple"]
            }],
            option:{
                title:{
                    display:true,
                    position:"bottom",
                    text: "Fruits"
                }
            }
        };
    },
  mounted(){
      var instance = this
      axios
      .get('https://infinite-ravine-97956.herokuapp.com/api/products')
      .then(function(response){

for(var i=0;i<response.data.data.length;i++){
    console.log(response.data.data[i].product_id)
instance.labels.push(response.data.data[i].product_id)
instance.datasets[0].data.push(response.data.data[i].price)}


      })
  }
};
</script>

