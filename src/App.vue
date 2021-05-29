<template>
  <div class="app">
    <div class="pokemonList">
      <header>
        <h1>{{config.application_name}}</h1>
      </header>
      <p>List of pokemon</p>
      <ul>
        <Pokemon
            v-for="character in this.characters"
            :key="character.name"
            :name="character.name"
            v-bind:url="character.url"
        />
      </ul>
      <div class="buttonList">
        <button v-on:click="trigger('next')">Next</button>
        <button v-if="this.offset > 0" v-on:click="trigger('prev')">Prev</button>
      </div>
    </div>
    <div class="characterList">
      <pokemonSearch/>
      <characterData/>
    </div>

  </div>
</template>

<script>
import './assets/App.css'
import './assets/characterData.css'
import './assets/queries.css'
import {mapState} from 'vuex'
import store from './store/store.vue'
import {Pokemon, characterData, pokemonSearch} from "./components";


store.commit({
  type: 'getCharacters'
})


export default {
  name: 'App',
  store: store,
  components: {
    Pokemon,
    characterData,
    pokemonSearch
  },
  methods:{
    trigger : function (button){
      button = button.toLowerCase();
      switch(button){
        case 'next':
          store.commit('nextPage')
          break;
        case 'prev':
          store.commit('prevPage')
          break;
      }
    }
  },
  computed: mapState({
    characters : state => state.characters,
    offset: state => state.offset,
    config: state => state.config,
    characterData: state => state.characterData
  })
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
