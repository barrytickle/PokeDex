<script>
import Vue from 'vue'
import Vuex from 'vuex'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)
Vue.use(Vuex)

const store = new Vuex.Store({
  state:{
    characters: [],
    characterData: [],
    offset: 0,
    config:{
      application_name: 'PokeDéx',
      api_url: 'https://pokeapi.co/api/v2',
      search_url: 'https://pokeapi.co/api/v2/pokemon/'
    },
  },
  mutations:{
    getCharacters(state, payload){

      //will check if the payload is an integer, and it will check if it's 0 to avoid confusion with bool
      if(parseInt(payload.offset) || parseInt(payload.offset) === 0){
        state.offset = payload.offset;
      }
      Vue.axios.get(`${state.config.api_url}/pokemon?limit=20&offset=${payload.offset ? payload.offset : state.offset}`)
      .then((res) => {state.characters =  res.data.results})
    },
    nextPage(state){
      const offset = state.offset + 20;
      store.commit({
        type: 'getCharacters',
        offset: offset
      });
    },
    prevPage(state){
      const offset = state.offset - 20;
      console.log('Function offset: ' +offset);
      store.commit({
        type: 'getCharacters',
        offset: offset
      });
    },
    getCharacterData(state, payload){

      console.log(payload.url);

      store.commit('clearCharacterData');

      if(!payload.url){
        throw 'No URL has been provided';
      }
      Vue.axios.get(payload.url).then((res) => state.characterData = res.data)
    },
    clearCharacterData(state){
      state.characterData = [];
    }
  }
});


export default store

</script>