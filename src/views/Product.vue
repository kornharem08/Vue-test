<template>
  <div>
    <h1>Product List</h1>
     <b-row>
      <b-col md="6" class="my-1">
        <b-form-group horizontal label="Filter" class="mb-0">
          <b-input-group>
            <b-form-input v-model="filter" placeholder="Type to Search" />
            <b-input-group-append>
              <b-btn :disabled="!filter" @click="filter = ''">Clear</b-btn>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col>
       </b-row>
       
    <b-table striped hover :items="products" :fields="fields" :per-page="pageSize" :current-page="pageIndex"  :filter="filter"></b-table>
    <b-pagination align="center" size="lg" :total-rows="products" v-model="pageIndex" :per-page="pageSize">
    </b-pagination>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'product',
  components: {
    
  },
  data(){
      return{
          message: 'Project22'
      }
  },
   data(){
      return{
          message: 'Project2',
          products: [],
          pageSize: 10,
          pageIndex:1,
          filter: null,
           fields: [ 
               {
                   key:'product_id',
                   sortable :true
               },
               {
                    key:'title',
                   sortable :true
               },
              
               {
                    key:'price',
                   sortable :true,
                   variant: 'danger'
               },
                 {
          key:  'show_details'  
        }     
               ],
      }
      
  },
   computed: {
    sortOptions () {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => { return { text: f.label, value: f.key } })
    }
  },
  mounted(){
      var instance = this
      axios
      .get('https://infinite-ravine-97956.herokuapp.com/api/products')
      .then(function(response){
console.log(response.data)
instance.products =response.data.data
      })
  }
}
</script>