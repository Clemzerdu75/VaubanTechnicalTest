<template>
  <div class="Main">
    <List :characters="characters" :expand="expandPersonnal"/>
    <PersonnalList :characters="characters" :expand="expandPersonnal" v-on:handleExpand="expandPersonnal = !expandPersonnal"/>
  </div>
</template>

<script>
import List from './mainPages/List'
import PersonnalList from './mainPages/PersonnalList'
import { characters } from './../data/characters'

characters.map((el) => {
  el.selected = false
  return(el)
})

export default {
  name: 'Main',
  data () {
    return {
      characters: characters,
      expandPersonnal: false,
    }
  },
  components: {
    List,
    PersonnalList
  },
}
</script>

<style scoped>
  .Main {
    display: flex;
    flex-direction: row;
  }
</style>
