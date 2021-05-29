<template>
  <div class="searchBar">
    <input
        v-on:keyup="searchCharacter(searchData)"
        v-model="searchData"
        v-bind:class="searchData.length === 0 ? '' : Object.keys(characterData).length > 0 && searchData.length > 0 ? 'found' : 'notFound' "
        type="text"
        placeholder="search"
    />
  </div>
</template>

<script>
import store from '../store/store.vue'
import {mapState} from "vuex";
export default {
  name: 'Pokemon',
  store: store,
  props:{
    name: String,
    url: String
  },
  data: function() {
    return {
        searchData: ''
      };
  },
  methods: {
    searchCharacter : function(url){
      if(url.length === 0){
        store.commit('clearCharacterData')
      }else{
        url = store.state.config.search_url + url;
        console.log(url);
        store.commit({
          type: 'getCharacterData',
          url : url,
        })
      }
    }
  },
  computed: mapState({
    characterData: state => state.characterData
  })



}
</script>