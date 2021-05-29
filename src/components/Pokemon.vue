 <template>
     <li :key="name" v-on:click="getCharacterData(url)">{{name}} </li>
 </template>

 <script>
 import store from '../store/store.vue'
 export default {
   name: 'Pokemon',
   store: store,
   props:{
     name: String,
     url: String
   },
   methods: {
     getCharacterData : function(url){
         store.commit({
           type: 'getCharacterData',
           url : url,
         })

     }
   }

 }
 </script>