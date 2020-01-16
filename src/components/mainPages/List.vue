<template>
<div class="Wrapper"
  v-bind:style=" expand ? 'width: 70%' : 'width: 100%' ">
  <h1 :style=" expand ? 'width: 69%' : 'width: 100%' ">STAR WARS CHARACTERS</h1>

  <div class="searchField">
    <img :src="require('./../../assets/searchWhite.png')" />
     <input type="text" v-model="search" placeholder="Search names"/>
  </div>

  <div class="List">
    <div v-for="character in filteredList" :key="character.name">
      <CharacterCard :character="character"/>
    </div>
  </div>
</div>
</template>

<script>
import CharacterCard from './../characterDisplay/CharacterCard';

export default {
  name: 'List',
  props:['characters', 'expand'],
  data () {
    return {
      search: '',
    }
  },
  components: {
    CharacterCard
  },

  computed: {
    filteredList() {
      let filtered = this.characters.filter(el => {
        return el.name.toLowerCase().includes(this.search.toLowerCase())
      })
      return filtered
    }
  }
}
</script>


<style scoped>

  .Wrapper {
    transition: .4s ease-out;
    min-width: 500px;
  }

  .Wrapper h1 {
    position: fixed;
    background-color: #0f0f0f;
    z-index: 50;
    padding-bottom: 30px;
    margin-top: -100px;
    padding-top: 120px;
    transition: .4s ease-out;
    min-width: 500px;
    color: yellow;
  }
  
  .List {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    animation-name: enter;
    animation-duration: .8s
  }

  .reduce {
    width: 50%;
  }

  .searchField {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin: 0 auto;
    width: 40%;
    margin-top: 8em;
    margin-bottom: 50px;
    animation-name: enter;
    animation-duration: .8s
  }

  .searchField input {
    width: 80%;
    border: none;
    border-bottom: solid 2px white;
    outline: none;
    font-size: 1.5em;
    color: #f0f0f0;
    background-color: transparent;
  }

  ::placeholder {
    font-size: 1em;
    color: grey;
  }

  .searchField img {
    width: 50px;
    margin-right: 10px;
  }

  @keyframes enter {
    0% {opacity: 0}
    50% {opacity: 0}
    100% {opacity: 1}
}
</style>
