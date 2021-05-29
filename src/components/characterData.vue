<template>
  <div class="characterData">
    <p v-if="Object.keys(characterData).length === 0">Please click a character to view data</p>
    <div v-if="Object.keys(characterData).length > 0" class="characterBoxTemplate">
      <div class="characterImage">
        <img
            v-bind:src="characterData.sprites.front_default"
            v-bind:alt="characterData.name"
        />
      </div>
      <div class="characterDetails">
        <div class="characterStats">
          <h3>{{characterData.name}}</h3>
          <p>Weight: {{characterData.weight}}kg</p>
          <p>Height: {{characterData.height}}cm</p>
        </div>
        <div class="characterAbilities">
          <h3>Abilities</h3>
          <ul class="abilityList">
            <li
                v-for="ability in characterData.abilities"
                v-bind:key="ability.name"
            > <span>{{ ability.ability.name }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import store from '../store/store.vue'
import {mapState} from 'vuex'

export default {
  name: 'characterData',
  store: store,
  computed: mapState({
    characterData: state => state.characterData
  })
  }
</script>